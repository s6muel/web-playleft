---
title: "Weather API - Understanding the init process"
date: 2025-11-24
description: "An overview of the Weather API's initialisation proccess."
tags: ["weather api"]
summary: "An overview of the Weather API's initialisation proccess."
toc: true
---
## Introduction
The initialisation process is designed to bootstrap infrastructure required for platform services. Specifically this includes:

-   Creation of data directories for all required active domains (i.e., `stations` and `observations` for MVP release);
-   Initialise database tables with BOM shapefile data via ETL pipeline; and
-   Upgrade table schemas to latest Alembic migration.

Notably this bootstraps the `stations` domain table `idm00013` from the same named BOM shapefile dataset. This is important because - aside from serving `stations` queries - endpoints that rely on station lookups depend on this table in order to perform KNN calculations.

## Requirements for infrastructure

-   **Domain directories:** The `StorageManager` requires existing directories for the respective domain before performing actions. Given `sm` is the basis for all IO operations, this is necessary.
-   **Shapefile to table processing:** At this stage, only the `idm00013` table is initiated with a shapefile dataset from BOM as it's source. The entire ETL process therefore requires a dataset from BOM's FTP server. To fulfill this requirement, we make a `BootstrapRequest` to the `CycleCoordinatorService` for handling.
    
    After acquiring the dataset, `InitialiseTableWithShapefile` can then process the `<dataset>.zip` in the ETL, it's result being a reproduction of the dataset in our PostgreSQL table.
-   **Upgrade table schemas via Alembic:** Once all tables have been initialised, we need to insure our database schema is up to date with our latest Alembic migration. We rely on the `MigrationsService` to process this request.

## Design

### Introduction (`InfrastructureInitialiserService`)

The initialisation process was designed to utilise existing services to complete a variety of functions to satisfy the infrastructure requirements described above. Additionally we introduce new services for functionality such as creating directories, formalising the shapefile ETL pipeline, and managing Alembic.

Given this process requires multiple interractions with different services, a single point of entry has been created for the init service container at `app/infrastructure/intitialise/`. This is made possible with a facade pattern service called `InfrastructureInitialiserService`, which provides a simple `run()` method that orchestrates the entire infrastructure initialisation process.

This new facade service provides a simple interface for the `InitialisePlatform`, `InitialiseTableWithShapefile`, and `MigrationsService` via the `run()` method. Each service is injectable on instantiation which means our initialisation entry point doesn't have to worry about service dependencies, only how to run and parse boolean results. This also allows us to easily swap out or add new services in the future.

### Stage 1: Initialise platform (`initialise_platform` module)

This module contains the `InitialisePlatform` class and provides the `create_platform_dirs()` static method. We import the `ACTIVE_DOMAINS` and `DATA_DIR` from `config.py` and then create all directories as defined by `ACTIVE_DOMAINS`, as in `/<DATA_DIR>/ACTIVE_DOMAINS[0:-1]`.

This process is idempotent in the sense that on each application startup, this process will not duplicate paths, only creating what is missing. All results are reported - no matter the outcome (i.e., skipped, failed, initialised) - in an `InitialisePlatformResults` pydantic object, which is included as apart of the `InitialisePlatformOutcome` object as `results`. This object also contains a `success` boolean object for efficient service interpretation. Results are also logged just in time and on completion for easy review.

### Stage 2: Initialise database (`initialise_db` module)

This module contains the `InitialiseTableWithShapefile` service and provides an interface via the `run()` method. Each request will need to come with an `InitTableSchemaContract`. This contract defines the requested `table_name`, the domain responsible for the table, the expected absolute path to the shapefile source data, the FTP path to the shapefile data, and a `BootstrapRequestContract`.

The service therefore provides a facade for an idempotent ETL pipeline that handles BOM shapefile datasets. The results is a faithful reproduction of BOM shapefile datasets into a PostgreSQL table with spatial index search capabilities.

#### Dependencies

-   `DatabaseService.get_database_service` to provide db connections.
-   `StorageManager` for pre-start checks (i.e., check current active paths for a domain)
-   `SyncCoordinator` to sync datasets from BOM FTP using a `BootStrapRequestContract`.
-   `SpatialDataProcessor` to extract, transform, and load shapefile datasets to the db as a table.

### Stage 3: Upgrade table schemas to head (`MigrationsService`)

The migrations service, located at `app/services/migrations_svc`, was introduced to provide an interface for Alembic's API. It allows for programmatic usage of commonly used Alembic functions, such as `alembic upgrade head` via the `upgrade_to_head()` method.

#### Dependencies

-   Configured `alembic.ini` at `/opt/alembic.ini`
-   Alembic `Config` object preconfigured with our `alembic.ini`
-   `DatabaseService.get_database_service` to provide db connection.
