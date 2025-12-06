+++
title = "Gleemacs"
date = "2025-11-14"
description = "My personal GNU Emacs configuration."
summary = "My personal configuration for GNU Emacs."
layout = "single"
tags = ["emacs"]
modified = "2025-12-05"
+++


> There&rsquo;s happiness :), and there&rsquo;s *gleemacs* =D.

**Last revised and exported on 2025-12-05 10:32:16 +1100}.**

This is my personal configuration for the awesome GNU Emacs! I built it from the
ground up with two blank files in a directory named `~/.gleemacs`, a metric shit
tonne of reading through `C-h v/f/P/m/k`, and the equivalent volumetric weight in
coffee. Eventually it grew into this living document. I created it because I
want to know my setup inside and out. After 5 weeks with DOOM Emacs, I had a
clear idea of both what was possible with Emacs and what I needed in my
workspace. So I set out to write my own and started with research and review of
[configs in the wild](#h:8fef9093-687f-44c8-9208-b18b9a733dbd).

For me, those configurations were instrumental in learning vanilla Emacs. As I
read through them, I would `C-h` each variable or function with my init files in
a split window. If it met my needs, improved performance, or made me smile, it
went in. This proved extremely useful for two reasons: I gained an understanding
of what settings I really needed and what they did, while learning to use Emacs
in it&rsquo;s vanilla state.

This experience was a positive *Emacs*-loop. The most useful of all being my
finagling of the built-in help functionality. Once you learn it, all of a sudden
the thing you want to change can be found on your own. In my opinion this is
more valuable than learning lisp itself when you&rsquo;re new to Emacs (or maybe this
is just an excuse for getting lost in parentheses&#x2026;).

*gleemacs* is thus built on the shoulders of giants. It&rsquo;s the result of
research, curation, and personalisation. It&rsquo;s performant, persistent, and
hygienic. It&rsquo;s easy to maintain and traverse, and is fuelled by practicality,
essentialism, and good old fashioned fun.

Please enjoy :)


**Table of Contents**

1.  [Overview](#h:53051a94-cd3d-4ca9-92f4-24343a62ef99)
2.  [Preface](#h:dda722ed-43c1-4c82-bf95-fec6a1cbe575)
    1.  [Why](#h:24ef5461-6dff-4e5f-884e-c9a897e22dfb)
        1.  [Context](#h:48f7f08e-e27d-46ef-b6ba-45d63cb7f1f2)
    2.  [Philosophy](#h:bd701525-44d6-46a3-af09-9691c0a31b7e)
        1.  [Ice Ice Baby!](#h:e1e7a974-f083-4442-b38b-37821f12d2e7)
        2.  [Performance](#h:07de5dae-b36d-43bb-b636-dec42d66d5bb)
        3.  [Persistence](#h:c6212343-e682-4016-9eec-331fa0b30c3c)
        4.  [Hygiene](#h:507a300e-d1a7-45d4-8a25-b04ab61798be)
        5.  [Privacy](#h:afd8b988-d574-46ac-955a-d497eae7304f)
3.  [Tangle me](#h:1bd5c3cc-43b8-4e6f-aeb2-84d1718a98ae)
4.  [Prepare for lisp off! (`early-init.el`)](#h:35b16a60-fd13-4500-bd36-a05e1ff77688)
    1.  [Header](#h:91dc1d6a-3f6b-443e-981a-34427f9b0e18)
    2.  [Performance Handling](#h:4f2257e5-0132-4101-9133-3b7a8b4c7b7b)
    3.  [Frame settings](#h:ae1fca7d-a7ca-4978-91dc-fb9452e23d04)
    4.  [Packages](#h:29b37f34-79f0-4d97-a94b-69ad0388de70)
    5.  [Footer](#h:2b7f1e07-e217-4ad6-8677-03e8310bcf95)
5.  [Let&rsquo;s get you ready for work (`init.el`)](#h:63a3b715-479d-4ba9-a27f-88db2f1c8e08)
    1.  [Header](#h:fa9434a4-71bc-4d2c-a117-273199097307)
    2.  [Package management](#h:6ba463a1-7615-4ed1-a89f-f5e06d6dcaa0)
        1.  [Enable native package compilation](#h:95362c25-6588-4f2f-be4c-8cad9930d05a)
        2.  [Setup `package`](#h:2512efe7-e5bc-48aa-bab2-d8bf34320deb)
        3.  [Setup `use-package`](#h:57b5d88c-d640-4a13-ac87-803c548a836a)
    3.  [Security settings](#h:ce4d8a73-eea5-4fff-9b4a-be3daee0edf0)
    4.  [Setup `*scratch*` buffer mode](#h:a8bd481c-c22f-4a99-a707-53288d12c2c8)
    5.  [Dynamic garbage collection with `gcmh`](#h:5ff25138-2daf-49d6-9db1-8e9991c7b817)
    6.  [Setup `modus-themes`](#h:c2f57382-2051-4268-9380-e71a772dbd33)
    7.  [Configure custom fonts](#h:f143555e-440f-4589-94bc-cb8ecab7778a)
    8.  [Disable line numbers (mode specific)](#h:938a6d59-415d-4827-9d4e-ba78eb577709)
    9.  [Set default `fill-column` width](#h:f4dcfa68-cc33-4163-af4c-9ba090ca0f35)
    10. [`which-key` was it again?](#h:dbdbf8ed-8999-4525-b0f2-a4542de22bb6)
    11. [Emacs tweaks](#h:b24ee109-23e4-4bfb-8b83-99b8e7eba8da)
        1.  [Disable lockfiles](#h:c6bcd8f2-1303-4f19-b91d-aafb20f57476)
        2.  [`custom.el` be gone!](#h:9276394b-cbaf-4c3d-b6c2-a1ab11ff1dab)
    12. [Require gleemacs modules](#h:7e76e4c7-7110-43aa-99f5-45c73c8ede2f)
6.  [Welcome to the house of glee (*gleemacs* modules)](#h:166c7b83-0b4c-4a99-a99a-f112621ba71e)
    1.  [`gleemacs-auth`](#h:256acaa3-01eb-4124-90f8-9301afe362f0)
        1.  [Header](#h:c44cf259-09cb-4bcd-aaf0-6751ed32a3f2)
        2.  [`auth-source`](#h:e38965aa-74c8-418e-8f79-922efb9bcd04)
        3.  [Set `user-full-name`](#h:bd322906-bede-42cb-8399-56de650b36b4)
        4.  [Set `user-email-address`](#h:8897861c-ab39-45a1-a3ef-48f75435d6f8)
        5.  [Footer](#h:65e5d34a-6fba-4756-9d90-14e61113c679)
    2.  [`gleemacs-completion`](#h:980eafe5-4b26-415d-8738-6f7450c0afd2)
        1.  [Header](#h:e2a47336-d2ed-403b-8811-b4e3bdf6cde7)
        2.  [`vertico`](#h:85798d37-a2d9-48b7-8e33-f7a14d111d0f)
        3.  [`orderless`](#h:9b6105ed-8ae3-4617-adf4-cb850094e02e)
        4.  [`minibuffer`](#h:5441ef86-9e1e-4cbd-a5f2-6a3c1f5591d7)
        5.  [`dabbrev`](#h:9d423ab9-41cc-4a31-8479-a2a62b4abd39)
        6.  [`corfu`](#h:5fdf3884-a37d-4335-abc3-452151e99ed8)
        7.  [`consult`](#h:81d93f7b-a77e-4bb3-b361-71d038d1c561)
        8.  [`embark`](#h:6b8551e8-f759-4587-9025-9f68108165c1)
        9.  [`embark-consult`](#h:d3069adc-ceae-4c81-8775-badb11120799)
        10. [`marginalia`](#h:7c14d1bf-c821-4d83-b6f9-f528c26e1ddc)
        11. [Nerd icons for `marginalia`](#h:c0c9d708-8650-49f3-8d79-65b4397bbcd7)
        12. [`yasnippet`](#h:d4d6c42f-a5f0-4905-b691-98d29216e5bc)
        13. [`yasnippet-snippets`](#h:f9afdabe-ae42-4206-ad49-113ec0c34272)
        14. [Footer](#h:58c6ea8f-8cbb-419e-870f-6e7d74091d84)
    3.  [`gleemacs-denote`](#h:f0b6e819-48c4-426f-ac6b-d47c0a235e7b)
        1.  [Header](#h:803a2d06-e3a3-465d-b407-b3964fac17c8)
        2.  [`denote`](#h:1e06e325-83ea-4ce6-bf24-32bfdb751769)
        3.  [`denote-journal`](#h:871bbef8-ae1e-4862-89b1-bd10236d40d6)
        4.  [Footer](#h:2afb941f-4e89-4b0c-bbef-569e89296457)
    4.  [`gleemacs-dired`](#h:ecd9dbed-0146-4d05-a49f-7688fe89e20d)
        1.  [Header](#h:7a7e9e1b-b255-4929-a9db-f6adc9714e95)
        2.  [`dired`](#h:c91fd2c6-4293-4a88-bb82-32e246381e56)
        3.  [`dired-subtree`](#h:d0980651-f735-47b5-83b1-9babeb6f2efa)
        4.  [Nerd icons for `dired`](#h:f8205753-6e96-44f9-8bd4-d0424fd45b99)
        5.  [Footer](#h:329aa092-fe8d-4c6a-8393-05dfab9969e5)
    5.  [`gleemacs-eglot`](#h:364049fb-8890-4987-82ad-9eb83a775d99)
        1.  [Header](#h:df497911-70b1-4420-aee7-a4292f3c068b)
        2.  [`eglot` and `basedpyright`](#h:471c68b9-6dd0-4a59-b0cc-5235221d4650)
        3.  [`consult-eglot`](#h:1beed37e-a196-409f-8072-746142b48414)
        4.  [`eldoc`](#h:99e9fea9-cb8f-4a24-89bf-2d62b99d7247)
        5.  [`eldoc-box`](#h:96144615-3be1-4cca-99ae-d7bc28296237)
        6.  [Taming `eglot` hints](#h:cb207868-3b28-40d3-998e-642bdd4981c3)
        7.  [Footer](#h:3cb7e4b6-79c3-4969-98a3-3e772ec20b47)
    6.  [`gleemacs-email`](#h:56e960b9-260e-4224-a0c3-4ca5089a5288)
        1.  [Header](#h:fe4b44b9-130d-4abd-aa96-d0fdfd11b0e8)
        2.  [`message`](#h:9761fcad-8f24-4203-bfc0-47d6800629c0)
        3.  [`smtpmail`](#h:d5fc5720-4999-4022-bd3b-010d6ac25160)
        4.  [`notmuch`](#h:fe79d830-af9b-4208-8e22-143180fdabaf)
        5.  [Footer](#h:efe915b0-87ec-451f-8e33-1a714484c96e)
    7.  [`gleemacs-essentials`](#h:0f9e3288-97a6-434e-80b4-ebc231ef68a1)
        1.  [Header](#h:3138aad9-2507-48b6-8833-75a2347b21f2)
        2.  [`emacs` settings](#h:d4fa3323-709f-48da-87b8-b1091167a07e)
        3.  [`diminish`](#h:633f6502-cf8a-4b33-9420-fd07ce8f43b3)
        4.  [`recentf`](#h:26522f14-b8f6-43d5-b422-dc07a49e8aa8)
        5.  [`savehist`](#h:1f755079-5ac9-44a8-a6ec-d2d4e67c4c1d)
        6.  [`save-place`](#h:aad225b9-a2f8-43e7-8720-e36ed5c6cca8)
        7.  [`mouse`](#h:eea0d09b-94fb-470a-b842-6c6cd231f936)
        8.  [`autorevert`](#h:56bef50e-b68e-4511-9b2f-ee91f22b80d2)
        9.  [`delsel`](#h:d724e6d3-5b33-410d-b4f5-82bf5ebbdac9)
        10. [`tooltip`](#h:1244202f-0ad5-4298-b820-296c9d567a79)
        11. [`no-littering`](#h:a3b250bb-e279-442a-b9e1-41e3f1972414)
        12. [Send backup files to `no-littering`](#h:7b619f6f-276e-426e-b0c5-f31aa2258965)
        13. [`undo-fu`](#h:d25b714c-8454-4dea-a2fc-688c5ed22bf7)
        14. [`undo-fu-session`](#h:42d4c972-a186-478f-8459-e6b845e6428a)
        15. [`server`](#h:26e3a7a8-2d2e-460e-a571-7c27e157ea0d)
        16. [`keyboard-quit` DWIM](#h:38ec5c6b-dc2e-4255-8573-7803d72209bc)
        17. [`nerd-icons`](#h:76f10d20-34fb-4cf0-ad71-b97a8748c155)
        18. [`dashboard`](#h:8d333d93-c176-47eb-bfbd-28b2474b0b4a)
        19. [`ibuffer` improvements](#h:3e5b5870-9fcf-4148-9fe4-4ff49f8eb440)
        20. [Replace `list-buffers` with `ibuffer`](#h:39010b7a-776c-49e9-8f54-25655514a601)
        21. [Nerd icons for `ibuffer`](#h:1caab0d9-f479-4276-904e-0622027768b7)
        22. [Footer](#h:a5894071-9977-44d8-8262-13a4d9a6a466)
    8.  [`gleemacs-flymake`](#h:a10f4b83-b0b2-4306-9a0e-a21790378a9c)
        1.  [Header](#h:d6b0d7f6-6317-49df-8e85-1d12094b352c)
        2.  [`flymake`](#h:e093d306-a762-464d-9785-28160030990e)
        3.  [`flymake-flycheck`](#h:b3d33660-fbfd-44d8-a787-5c1d4bcd9a20)
        4.  [Footer](#h:688d447a-1237-4fc4-a8d8-f507593be547)
    9.  [`gleemacs-git`](#h:cfd83654-5a5a-4fcb-a73c-873ee94c640f)
        1.  [Header](#h:e04fc654-76e0-43b8-abd6-6f8b86534365)
        2.  [`project`](#h:2598412a-c086-427f-b907-d3cac8ec7abc)
        3.  [`transient`](#h:33f332b5-0e61-40fe-8149-fafbfdbd5be8)
        4.  [`magit`](#h:7b29aa9e-dbbf-4529-a877-4b2f60fa3263)
        5.  [`magit-repos`](#h:14dafaa6-f211-4915-acf0-e896ff8fbe9a)
        6.  [`diff-hl`](#h:4decf0f8-2f1d-429c-9f5f-01e7d9b796b5)
        7.  [Footer](#h:4734c810-5628-4980-a4e0-95959622cdc4)
    10. [`gleemacs-helpers`](#h:636cea02-f3c5-4a3c-8ad6-7107ffda3c14)
        1.  [Header](#h:ad02ef8f-955f-4bb3-89e4-552bcfa993f3)
        2.  [`gleemacs-helper-auth-get-field`](#h:be40964e-8203-4630-b1fd-28c505cc25fe)
        3.  [Footer](#h:66df97ea-6162-4df2-9942-f143fa66bfd6)
    11. [`gleemacs-irc`](#h:1ee51d4d-54c1-463f-859c-80291e000f36)
        1.  [Header](#h:5e8b7974-a1cc-4981-b7e1-1dc3a5d621cf)
        2.  [`erc` setup](#h:12b5a267-5dfe-408e-a3d2-9ab2024695d6)
        3.  [`erc-libera-connect`](#h:01947a1a-509f-4e8f-815f-e9c38200b0e3)
        4.  [Footer](#h:e8cea086-9796-44b1-8eab-eec63fd426fb)
    12. [`gleemacs-keybindings`](#h:28d03a5b-c2d1-47f1-9bcb-0eabaf390d21)
        1.  [Header](#h:fb8b5aa9-3c2b-498d-bffa-13b3fdba5c22)
        2.  [override and adjust `emacs` defaults](#h:5f1e71cc-5a01-4b5a-9c40-c8e87b69b125)
        3.  [`org`](#h:e7094933-cc3e-460b-8f08-65c988d62843)
        4.  [`general`](#h:bbf7582f-15aa-4dfb-8abe-365a56d1686e)
        5.  [Footer](#h:02a18d18-174c-4c93-b823-20be30b25b4f)
    13. [`gleemacs-markdown`](#h:3aa88b4e-bc43-4601-87f7-4d873b682284)
        1.  [Header](#h:e44aef34-2462-4821-a3d8-9841c1774fa4)
        2.  [`markdown-mode`](#h:424d0663-3631-4c7c-a15e-e8e606248ac0)
        3.  [`markdown-toc`](#h:5352989a-d87e-4a37-a966-e3b74443c94a)
        4.  [Footer](#h:10e8198c-9171-40e0-886a-41c862ef6f2b)
    14. [`gleemacs-languages`](#h:e7ecab49-b5dc-4a79-8c7b-ea34283bbc03)
        1.  [Header](#h:3b22c03b-99b7-4345-a51a-60b4df54c80b)
        2.  [`treesit`](#h:453aea7d-dc31-4d29-b0f9-1abef1ac9d16)
        3.  [`text-mode`](#h:9d320186-fbf2-4133-aa52-ca5af7da103d)
        4.  [Settings for common file types](#h:fcb18d03-aa56-421e-a162-47b127c27f59)
            1.  [`PKGBUILD`](#h:f9f334ba-ab90-4781-bc31-4e674a194d5d)
            2.  [`systemd` and `.conf` files](#h:092260fc-c4ec-412d-b9db-6f42c2eff2e0)
        5.  [Footer](#h:1cb7c234-5a1d-4dd5-a057-9ccb08ff4b94)
    15. [`gleemacs-org`](#h:6653a561-f152-4d5f-83b2-fb5281d9de84)
        1.  [Header](#h:5439ad83-a951-4788-881b-9b0847cd9bf4)
        2.  [`australia-holidays`](#h:4ef90aa0-40f0-4704-8c3a-94a5e8779835)
            1.  [Add daylight savings time](#h:6e5f1be3-c0f4-4a27-ae66-9e18a5d4d3df)
        3.  [`calendar`](#h:9b1bb859-a811-46f8-afaa-d13a9ae9f337)
        4.  [`org`](#h:8605aa5c-86d0-49fe-8d9e-a3cb90213f5c)
            1.  [Org general settings](#h:a3b098a1-ea22-4385-b44b-b3d19c23ac2b)
            2.  [Org indentation settings](#h:7df0c93a-20be-4e4c-b72a-8f758ec41d45)
            3.  [Org todo and refile settings](#h:8492d68e-b711-4204-91bf-ba99d4fb9408)
            4.  [Org links](#h:47c08a20-0133-4565-a3cc-d69febae1c3c)
            5.  [Org codeblock settings](#h:2016204b-69ee-46ba-a5dd-cdb08c8ef460)
            6.  [Org export settings](#h:f7156605-dbbc-40d2-abff-396b13bc962e)
            7.  [Setup project-based note taking](#h:c22df481-ccb9-4e19-94ab-e6b2c0c6f9b1)
            8.  [Setup capture templates](#h:4dd2e73f-d6aa-4e9f-8edd-23a627c4afa5)
            9.  [Custom function `gleemacs/org-assign-custom-ids`](#h:5044085c-0a6a-4ad7-ab22-69c5109ef035)
            10. [](#h:4b2fd9db-9373-4ce1-86b7-b9a801882337)
        5.  [`org-superstar`](#h:739682b4-1f1e-43df-8f1d-711957de87d3)
        6.  [`org-tempo`](#h:8741adc1-c6df-4d29-9b23-abacf218470e)
        7.  [`ox-gfm`](#h:69843e13-a6f8-4c84-991a-4002ebed33f9)
        8.  [Footer](#h:e58983a7-0f63-4e77-86b0-ec1834060ef9)
    16. [`gleemacs-python`](#h:be7c601e-e790-44c6-aa3c-33f2dc720995)
        1.  [Header](#h:e7e68f1c-45d9-46ff-9d87-35632f2f5463)
        2.  [General settings](#h:210cd552-be3e-4e7c-98f6-511c6ffeca64)
        3.  [`pyvenv`](#h:cb877ca4-c55d-497f-b2e7-bb2c005eda36)
        4.  [Footer](#h:f61fec5d-8c14-4f12-a865-912311d75560)
    17. [`gleemacs-rss`](#h:993722af-6bc3-4f03-a95d-f1135c1de22d)
        1.  [Header](#h:a41cad18-44bd-4ca0-bbb8-9c08420ac147)
        2.  [`elfeed`](#h:314d3429-ad83-4c3a-a15e-87f1d0ece6e8)
        3.  [`elfeed-goodies` setup](#h:5737ed1b-3140-4856-b308-a49f08741ffb)
        4.  [Footer](#h:412b5eb6-272a-4e21-af9a-00c9c5f88516)
    18. [`gleemacs-search`](#h:8c4a6980-dc81-4432-b1f9-c9be2dda56ec)
        1.  [Header](#h:52f06824-fb5f-45e8-a062-1c6fea118493)
        2.  [`isearch`](#h:b77b8d4c-0656-493e-8f10-d613730c5268)
        3.  [`rg` and `ripgrep` tooling](#h:f4a774ca-b1ee-47fc-a4ba-0f526ebc13ba)
        4.  [`re-builder`](#h:9e7c4a55-8045-4e6d-9720-5eb2bbb35b68)
        5.  [`xref`](#h:15401141-af3c-4a32-8028-8b0d43f8ab3e)
        6.  [`grep`](#h:a15faa9b-f6a8-4916-a2a0-85d946904a3c)
        7.  [Footer](#h:56e9dc83-b519-46dc-8dbd-c6b21375a8b2)
    19. [`gleemacs-spellcheck`](#h:236323c2-3e7f-49bf-8605-71ed41347ab3)
        1.  [Header](#h:32dd0b7f-6dbd-4790-8f7e-aaae7faf4e55)
        2.  [`flyspell`](#h:32041c31-7071-49ea-864d-674f67636932)
        3.  [`dictionary`](#h:8a648d54-a04b-41fc-b4c7-9e29b21ed9f5)
        4.  [`altcaps`](#h:65abd4c7-6306-4a9e-b97f-75f2e5542865)
        5.  [Footer](#h:99fc4262-588b-4994-b171-2c627842d727)
    20. [`gleemacs-terminal`](#h:2f3dd6c6-cf61-47e5-81fe-fd4dca219cb3)
        1.  [Header](#h:47d08db5-09c1-46c7-90c2-a13ece256098)
        2.  [`vterm`](#h:4464d571-3f13-4a38-997e-27e07adbbcaf)
        3.  [Footer](#h:aaf600ce-8b63-448e-858e-1e2d4fc6e58e)
    21. [`gleemacs-window`](#h:768f0eef-b96c-421a-be30-d77fa862661c)
        1.  [Header](#h:1ffef3fa-9036-41bd-a28e-809b8c0d4eda)
        2.  [Setting up where certain buffers appear](#h:5d16cd30-eb31-4b1e-a95b-3a027e319e91)
        3.  [*gleemacs* modeline setup](#h:5b641c02-9718-4dc6-be20-86bc7c8e96b9)
        4.  [`uniquify`](#h:dc83b0a8-dd7a-4a97-a64f-2d14b0362283)
        5.  [`ace-window`](#h:c21457dd-4585-4644-b7d6-73dcd792095d)
        6.  [`winner`](#h:008c887c-1e4b-47bd-8e12-10964e8e29c9)
        7.  [`tab-bar`](#h:017eae8e-db26-434e-b787-c622884ef08b)
        8.  [Footer](#h:9dae1c55-0ba0-4980-863d-b7f71a0cc91f)
7.  [Cheers and Inspiration](#h:8fef9093-687f-44c8-9208-b18b9a733dbd)


<a id="h:53051a94-cd3d-4ca9-92f4-24343a62ef99"></a>

# Overview

*gleemacs* has been built for:

-   **Programming:** IDE-like functionality for Python with `basedpyright`. Setup
    for handling Docker, bash, `PKGBUILD` files, and various data serialisation
    languages. Efficient version control with `magit`.

-   **Writing and note taking:** `org` and `denote` for efficient note taking and
    organised writing. Personal and project specific capture templates.

-   **Communication and information:** Emails using `notmuch`, `smtpmail` and an
    `mbsync` backend. RSS reading with `elfeed`. IRC with `erc`.

-   **Daily useage:** It&rsquo;s fast! File editing persistence and safety without
    pollution. Legible in all lighting conditions with `modus-themes`. Simplified,
    informative modeline.


<a id="h:dda722ed-43c1-4c82-bf95-fec6a1cbe575"></a>

# Preface


<a id="h:24ef5461-6dff-4e5f-884e-c9a897e22dfb"></a>

## Why

In essence, *gleemacs* exists because I want to know how my setup works. The
goal is to remove complexity while remaining easy to configure, maintain, and
traverse. When things go wrong, I can fix them without relying on someone else
(thanks, `C-h`!). After reviewing a lot of configs in the wild from [Protesilaos](https://protesilaos.com/emacs/dotemacs),
[Purcell](https://github.com/purcell/emacs.d), and [Cherti](https://github.com/jamescherti/minimal-emacs.d), it didn&rsquo;t feel like a mission to build what I had in mind.


<a id="h:48f7f08e-e27d-46ef-b6ba-45d63cb7f1f2"></a>

### Context

-   Experience with GNU Emacs at start of writing: ~6 weeks


<a id="h:bd701525-44d6-46a3-af09-9691c0a31b7e"></a>

## Philosophy


<a id="h:e1e7a974-f083-4442-b38b-37821f12d2e7"></a>

### Ice Ice Baby!

*gleemacs* is focused on vanilla GNU Emacs in terms of bindings and packages.
Mainly because I want to be able to use Emacs (generally) across systems without
too much friction, and it&rsquo;s my favourite flavour of ice cream. The fine print
being: &rsquo;leader key&rsquo; functionality is setup with the prefix `C-c` using
`general.el` (see the [`gleemacs-keybindings`](#h:28d03a5b-c2d1-47f1-9bcb-0eabaf390d21) module), but the goal is to be as
close to vanilla or default configurations as possible. That means you&rsquo;ll still
need to manually `M-x hanoi`, sorry!

Another reason for this is performance. For example, using the built in modeline
compared to using the `doom-modeline` package came with significant startup
improvements. 

Of course, I will utilise third party packages where their use far outweighs my
efforts in reproducing the functionality. In some cases, like the mode line for
example, investing effort in learning in-built functionality was worth the
performance gains.

I&rsquo;m happy to rely on the community to provide functionality that the
reproduction of which is well beyond my pay grade. At the end of the day I don&rsquo;t
want to engage in busy work either. I actually want to *use* Emacs, not
infinitely configure it.


<a id="h:07de5dae-b36d-43bb-b636-dec42d66d5bb"></a>

### Performance

Inspiration is taken from existing configurations to build a solid and performant setup. Typical startup improvements such as garbage collection, native compilation of packages, and other refinements are found in `early-init.el`. Dashboard functionality has also been implemented using the `dashboard` package located in the [`gleemacs-essentials`](#h:0f9e3288-97a6-434e-80b4-ebc231ef68a1) module. I rarely use the `*scratch*` buffer and like the utility that a dashboard brings with it.

Other notable features include:

-   the use of `gcmh` to manage garbage collection post start-up,
-   complete disabling of the vanilla startup screen (in addition to inhibiting it), and
-   run of the mill removal of GUI features, including GUI/GTK-based prompts.

Experimentation with different settings by addition, subtraction, or modification, did not yield a performance improvement that warranted inclusion. In my useage startup times vary from 0.3-0.4s and I&rsquo;m happy with that!


<a id="h:c6212343-e682-4016-9eec-331fa0b30c3c"></a>

### Persistence

My mind works better when I&rsquo;m able to get right back into something in the exact
context and configuration that I left it in. To achieve this, a combination of
`recentf`, `savehist`, `save-place`, `undo-fu` (see [`gleemacs-essentials`](#h:0f9e3288-97a6-434e-80b4-ebc231ef68a1)), and
`persp-mode` are used (see [`gleemacs-window`](#h:768f0eef-b96c-421a-be30-d77fa862661c)). The loading of perspectives on
startup are up to the user via `C-c p l`, as I prefer to have the option to
resume the perspective I was in or to start with a blank canvas.

-   2025-11-17: `persp-mode` is currently disabled as I didn&rsquo;t end up using it to
    it&rsquo;s full potential. I&rsquo;m now trying out `tab-bar` to visually separate
    workspaces which in practice suits my workflow better.


<a id="h:507a300e-d1a7-45d4-8a25-b04ab61798be"></a>

### Hygiene

Persistence requires writing data to disk, and by default Emacs thinks any
working directory is it&rsquo;s oyster, leading to a lot of stray `#files#` and a
cluttered `.emacs.d` folder. To keep our files tidy and organised, we disable
lockfiles in `init.el`, and utilise the `no-littering` package from the
[`gleemacs-essentials`](#h:0f9e3288-97a6-434e-80b4-ebc231ef68a1) module to manage persistent data.


<a id="h:afd8b988-d574-46ac-955a-d497eae7304f"></a>

### Privacy

To preserve the privacy of data like email addresses, IRC logins, and other
private information, *gleemacs* makes us of the `auth-sources` (see
[`gleemacs-auth`](#h:256acaa3-01eb-4124-90f8-9301afe362f0)). The idea is to be able to share or publicly store
configurations without leaking sensitive or otherwise private data. Additional
security enhancements are found in [security settings](#h:ce4d8a73-eea5-4fff-9b4a-be3daee0edf0) which mainly apply to IRC
and self-hosted web service setups (e.g., email with self-signed certificates).

Implementing out of the box reliance on `auth-sources` and the `.authinfo.gpg`
file encourages best practices when it comes to distributing sensitive
information. I also considered integrating this functionality using `pass`, but
it&rsquo;s overkill for my requirements at this stage.


<a id="h:1bd5c3cc-43b8-4e6f-aeb2-84d1718a98ae"></a>

# Tangle me

-   To evaluate, simply run `C-c C-v C-t`


<a id="h:35b16a60-fd13-4500-bd36-a05e1ff77688"></a>

# Prepare for lisp off! (`early-init.el`)

The early initialisation phase contains performance optimisations, disables the
inbuilt GUI, sets up package archives and `use-package`, and improves some basic
security settings. Prot graciously explained to me that this phase initialises
prior to Emacs drawing it&rsquo;s frame, and I&rsquo;ve therefore tried to arrange the
settings with this in mind.

These settings have been curated from other configs that offer the greatest
performance benefits. As a result, our `early-init.el` is rather short, but it
provides excellent performance!


<a id="h:91dc1d6a-3f6b-443e-981a-34427f9b0e18"></a>

## Header

    ;;; early-init.el --- Early Init -*- no-byte-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: "0.1.0"
    
    ;;; Commentary:
    ;;
    ;; The `early-init' is will run prior to Emacs rendering it's initial frame.
    ;; Therefore, strictly legal, performance enhancing substances should go here.
    ;;
    ;; Slow start up times make Sam go something something..
    
    ;;; Code:


<a id="h:4f2257e5-0132-4101-9133-3b7a8b4c7b7b"></a>

## Performance Handling

In my tinkering, the following settings were the most important when trying to improve startup times. As I briefly mentioned earlier, experimentation with a range of settings seemingly provided little to no benefit. Additionally, a lot of settings in use in other configs seem to be the default for Emacs when reading about them in `C-h v`, so I decided to leave them out. 

We do not reset our garbage collection settings because that&rsquo;s taken care of by `gcmh` after early initialisation. Read more about this in the [gcmh](#h:5ff25138-2daf-49d6-9db1-8e9991c7b817) section.

    ;; ; Performance Handling ---------------
    ;; Temporarily increase the garbage collection threshold.  These
    ;; changes help shave off about half a second of startup time.  The
    ;; `most-positive-fixnum' is DANGEROUS AS A PERMANENT VALUE.  See the
    ;; `emacs-startup-hook' a few lines below for what I actually use.
    (setq gc-cons-threshold most-positive-fixnum
          gc-cons-percentage 0.5)
    
    ;; Same idea as above for the `file-name-handler-alist' and the
    ;; `vc-handled-backends' with regard to startup speed optimisation.
    ;; Here I am storing the default value with the intent of restoring it
    ;; via the `emacs-startup-hook'.
    (defvar gleemacs--file-name-handler-alist file-name-handler-alist)
    (defvar gleemacs--vc-handled-backends vc-handled-backends)
    
    (setq file-name-handler-alist nil
          vc-handled-backends nil)
    
    ;; Process performance tuning
    (setq read-process-output-max (* 4 1024 1024))
    
    ;; ; Restore defaults after init
    (add-hook 'emacs-startup-hook
              (lambda ()
                (setq file-name-handler-alist gleemacs--file-name-handler-alist
                      vc-handled-backends gleemacs--vc-handled-backends)))


<a id="h:ae1fca7d-a7ca-4978-91dc-fb9452e23d04"></a>

## Frame settings

Mostly standard *Emacsen* settings here, such as disabling GUI and GTK related prompts, and preventing (not just inhibiting) the vanilla Emacs startup screen. There&rsquo;s not much to *see* here. ;)

    ;; ; UI Config ---------------
    ;; Don't show the splash screen
    (setq inhibit-startup-message t)
    
    ;; Suppress the vanilla startup screen completely. We've disabled it with
    ;; `inhibit-startup-screen', but it would still initialize anyway.
    (advice-add 'display-startup-screen :override #'ignore)
    
    ;; Remove "For information about GNU Emacs..." message at startup
    ;; Courtesy of James Cherti
    (advice-add 'display-startup-echo-area-message :override #'ignore)
      
    (tool-bar-mode -1)    ; Disable toolbar
    (scroll-bar-mode -1)  ; Disable scrollbar
    (menu-bar-mode -1)    ; Disable menu bar
    (set-fringe-mode 10)  ; Give fringe some space
    
    (column-number-mode)
    (global-display-line-numbers-mode 1)  ; Show line numbers
    
    ;; Disable GTK/GUI prompts and limit to minibuffer y/n
    (setq use-dialog-box nil)
    (setq use-file-dialog nil)
    (setq use-short-answers t)
    
    ;; Frame settings
    ;; Courtesy of Protesilaos Stavrou
    (setq frame-resize-pixelwise t
          frame-inhibit-implied-resize 'force
          frame-title-format '("%b")
          ring-bell-function 'ignore
          inhibit-splash-screen t
          inhibit-startup-screen t
          inhibit-x-resources t
          inhibit-startup-echo-area-message user-login-name ; read the docstring
          inhibit-startup-buffer-menu t)


<a id="h:29b37f34-79f0-4d97-a94b-69ad0388de70"></a>

## Packages

    ;; Prefer newest compiled files
    (setq load-prefer-newer t)
    
    ;; Initialise installed packages
    (setq package-enable-at-startup nil)


<a id="h:2b7f1e07-e217-4ad6-8677-03e8310bcf95"></a>

## Footer

    ;; End:
    
    ;;; early-init.el ends here


<a id="h:63a3b715-479d-4ba9-a27f-88db2f1c8e08"></a>

# Let&rsquo;s get you ready for work (`init.el`)

The initialisation phase (also see [early-init](#h:35b16a60-fd13-4500-bd36-a05e1ff77688)) is responsible for ensuring that
Emacs is performant and establishing a sound vanilla experience. `init.el`
notably contains packaging setup, garbage collection, and our aesthetic settings
like [selecting a theme](#h:c2f57382-2051-4268-9380-e71a772dbd33) and [our preferred font](#h:f143555e-440f-4589-94bc-cb8ecab7778a).

The focus during design was to minimise as much as possible any opinionated
influence outside of aesthetic choice. I learnt so much about Emacs reading it&rsquo;s
own documentation when researching other configurations. So *gleemacs* without
modules is a great environment for learning GNU Emacs without it being too
opinionated.

Additional functionality is added via [gleemacs modules](#h:166c7b83-0b4c-4a99-a99a-f112621ba71e) rather than managing one
large `init.el` file. This centralises configuration to the respective modules
and allows for easy maintenance and efficient customisation.


<a id="h:fa9434a4-71bc-4d2c-a117-273199097307"></a>

## Header

    ;;; init.el --- Initialise Gleemacs -*- no-byte-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; Now that the frame is rendered, we can start resetting some dangerous
    ;; performance settings from the `early-init' stage, and begin adding some
    ;; basic functionality.  In the case of `gleemacs', this means establish a
    ;; sound GNU Emacs environment that is perfect place to learn vanilla Emacs.
    ;;
    ;; If you were expecting chocolate Emacs, you will sadly be disappointed :(
    ;; Tea and biscuits are at the back.
    
    ;;; Code:


<a id="h:6ba463a1-7615-4ed1-a89f-f5e06d6dcaa0"></a>

## Package management


<a id="h:95362c25-6588-4f2f-be4c-8cad9930d05a"></a>

### Enable native package compilation

Here we enable native package compilation just in time compiling for significant performance improvements. Additionally, we silence any compiler errors on startup that, as I understand, are only useful to Emacs developers and not a real concern for users.

    ;; ; Package Management ---------------
    ;; Enable async native compilation
    (setq package-native-compile t
          ;; native-comp-deferred-compilation t  ; obsolete
          native-comp-jit-compilation t  ; supersedes above
          native-comp-async-report-warnings-errors nil)


<a id="h:2512efe7-e5bc-48aa-bab2-d8bf34320deb"></a>

### Setup `package`

    (require 'package)
    
    ;; Initialise installed packages
    (setq package-enable-at-startup t)

&#x2026; And prioritise our preferred archives.

    ;; Don't register packages as projects
    (setq package-vc-register-as-project nil) ; Emacs 30
    ;; Also read: <https://protesilaos.com/codelog/2022-05-13-emacs-elpa-devel/>
    (setq package-archives
          '(("gnu-elpa" . "https://elpa.gnu.org/packages/")
            ("gnu-elpa-devel" . "https://elpa.gnu.org/devel/")
            ("nongnu" . "https://elpa.nongnu.org/nongnu/")
            ("melpa" . "https://melpa.org/packages/")))
    
    ;; Highest number gets priority (what is not mentioned has priority 0)
    (setq package-archive-priorities
          '(("gnu-elpa" . 3)
            ("melpa" . 2)
            ("nongnu" . 1)))
    
    (package-initialize)
    (unless package-archive-contents
      (package-refresh-contents))


<a id="h:57b5d88c-d640-4a13-ac87-803c548a836a"></a>

### Setup `use-package`

We then setup `use-package` which is used exclusively throughout *gleemacs* from this point forwards.

    ;; Initialize use-package on non-Linux platforms
    (unless (package-installed-p 'use-package)
      (package-install 'use-package))
    
    (require 'use-package)
    (setq use-package-always-ensure t)
    (setq use-package-enable-imenu-support t)


<a id="h:ce4d8a73-eea5-4fff-9b4a-be3daee0edf0"></a>

## Security settings

It&rsquo;s notable that these settings may require additional configuration for self-signed certificates. In practical terms, this has only impacted `localhost` addressed web services in my experience, such as SMTP.

    ;; ; Security ---------------
    ;; Courtesy of James Cherti
    (setq gnutls-verify-error t)  ; Prompts user if there are certificate issues
    (setq tls-checktrust t)  ; Ensure SSL/TLS connections undergo trust verification
    (setq gnutls-min-prime-bits 3072)  ; Stronger GnuTLS encryption


<a id="h:a8bd481c-c22f-4a99-a707-53288d12c2c8"></a>

## Setup `*scratch*` buffer mode

Setting the `*scratch*` buffer&rsquo;s major mode to `fundamental-mode` improves startup performance effectively by limiting the dependencies (e.g., `flymake`) for a basic startup. *gleemacs* is also configured to display a simple [dashboard](#h:8d333d93-c176-47eb-bfbd-28b2474b0b4a) on startup. 

    ;;; Set `*scratch*' buffer to `fundamental-mode'
    (setq initial-major-mode 'fundamental-mode)


<a id="h:5ff25138-2daf-49d6-9db1-8e9991c7b817"></a>

## Dynamic garbage collection with `gcmh`

`gmch` dynamically adjusts garbage collection settings based on an idle delay.
In my experience the use of this package resulted in faster startup times than
restoring the garbage collection defaults in `init.el`. It also allows you to
adjust the minimum and maximum `gc-cons-threshold` in a similar fashion to
Emacs, so it felt reasonable to include this as a matter of performance.

    ;; ; Performance Tuning ---------------
    ;; This handles our garbage collection automatically when we're not using
    ;; Emacs. While I know that's insane to not use Emacs, but just know our trash
    ;; will be collected promptly, and a stated delay (inspiration: Local Council).
    (use-package gcmh
      :hook (after-init . gcmh-mode)
      :diminish gcmh-mode
      :custom
      (gcmh-high-cons-threshold (* 128 1024 1024))
      (gcmh-idle-delay 5))


<a id="h:c2f57382-2051-4268-9380-e71a772dbd33"></a>

## Setup `modus-themes`

Modus strikes the perfect balance between no syntax and looking like the results
of Homer&rsquo;s make-up gun experiment.

Prot provides functionality that allows for suitable themes in any environment
with the `mode-themes-toggle` and `mode-themes-rotate` functions. In bright
daylight conditions I&rsquo;ve found `modus-operandi` to be the most legible. As the
golden hour approaches or when it&rsquo;s overcast, I&rsquo;ll move to the `tinted` variant.
Finally, for low light I prefer `modus-vivendi-tinted` because my eyes seem to
suffer less stress than the non-tinted variant.

The default mapping for `F5` has been swapped to `modus-themes-rotate` so we can
rotate between the three themes as needed throughout the day. This is done
because `-toggle` (for now!) only supports two variants [which to clarify seems
reasonable given &rsquo;toggle&rsquo; implies binary functionality, whereas &rsquo;rotate&rsquo; implies
multiple options].

    ;; ; UI Config ---------------
    ;; Theme Setup
    ;; Modus Themes /co Protesilaos Stavrou
    (use-package modus-themes
      :ensure t
      :demand t
      :init
      ;; Starting with version 5.0.0 of the `modus-themes', other packages
      ;; can be built on top to provide their own "Modus" derivatives.
      ;; For example, this is what I do with my `ef-themes' and
      ;; `standard-themes' (starting with versions 2.0.0 and 3.0.0,
      ;; respectively).
      ;;
      ;; The `modus-themes-include-derivatives-mode' makes all Modus
      ;; commands that act on a theme consider all such derivatives, if
      ;; their respective packages are available and have been loaded.
      ;;
      ;; Note that those packages can even completely take over from the
      ;; Modus themes such that, for example, `modus-themes-rotate' only
      ;; goes through the Ef themes (to this end, the Ef themes provide
      ;; the `ef-themes-take-over-modus-themes-mode' and the Standard
      ;; themes have the `standard-themes-take-over-modus-themes-mode'
      ;; equivalent).
      ;;
      ;; If you only care about the Modus themes, then (i) you do not need
      ;; to enable the `modus-themes-include-derivatives-mode' and (ii) do
      ;; not install and activate those other theme packages.
      ;; (modus-themes-include-derivatives-mode 1)
      :bind
      (("<f5>" . modus-themes-rotate)
       ("C-<f5>" . modus-themes-select)
       ("M-<f5>" . modus-themes-load-random))
      :config
      ;; Your customizations here:
      (setq modus-themes-custom-auto-reload nil
            modus-themes-to-toggle '(modus-operandi-tinted modus-vivendi-tinted)
    	modus-themes-to-rotate '(modus-operandi
    				 modus-operandi-tinted
    				 modus-vivendi-tinted)
            modus-themes-mixed-fonts t
            modus-themes-variable-pitch-ui t
            modus-themes-italic-constructs t
            modus-themes-bold-constructs t
            modus-themes-completions '((t . (bold)))
            modus-themes-prompts '(bold))
            ;; modus-themes-headings
            ;; '((agenda-structure . (variable-pitch light 2.2))
            ;; (agenda-date . (variable-pitch regular 1.3))
            ;; (t . (regular 1.15))))
    
      (setq modus-themes-common-palette-overrides nil)
      ;; Finally, load your theme of choice (or a random one with
      ;; `modus-themes-load-random', `modus-themes-load-random-dark',
      ;; `modus-themes-load-random-light').
      (modus-themes-load-theme 'modus-operandi))


<a id="h:f143555e-440f-4589-94bc-cb8ecab7778a"></a>

## Configure custom fonts

I know exactly what you&rsquo;re thinking right now: &ldquo;this guy is cosplaying a Greek
philosopher!&rdquo; Not quite, but his influence is clear, and I cannot fault Prot&rsquo;s
aesthetic taste and focus on legibility. Aporetic is perfect for my needs
because of limited screen space and utilise window splits heavily in my
workflow. Years ago I tried Iosevka, but I could never get used to it. I would
revert to Hack or JetBrains Mono for their legibility, until I found Aporetic: a
compact Hack!

    ;; Setup fonts
    (set-face-attribute 'default nil
                        :height 130 :weight 'normal :family "Aporetic Sans Mono")
    (set-face-attribute 'fixed-pitch nil
                        :family "Aporetic Serif Mono")
    (set-face-attribute 'variable-pitch nil
                        :family "Aporetic Serif")


<a id="h:938a6d59-415d-4827-9d4e-ba78eb577709"></a>

## Disable line numbers (mode specific)

Don&rsquo;t like line numbers in some mode? No worries, here we define a list of `-mode-hook` to disable line numbers. To find a mode, `C-h m` in the buffer you want to check; once you know the mode, you can search using `C-h f` for the relevant hook function to append below. And just like that&#x2026; They were gone!

    ;; Disable line numbers for some modes
    (dolist (mode '(org-mode-hook
                    term-mode-hook
                    shell-mode-hook
    		vterm-mode-hook
    		notmuch-hello-mode-hook
    		notmuch-show-mode-hook
    		notmuch-tree-mode-hook
    		elfeed-show-mode-hook
    		elfeed-search-mode-hook
                    treemacs-mode-hook
                    eshell-mode-hook))
      (add-hook mode (lambda () (display-line-numbers-mode 0))))


<a id="h:f4dcfa68-cc33-4163-af4c-9ba090ca0f35"></a>

## Set default `fill-column` width

Set the default line width to 80 characters. If you write a particularly long
line in `org-mode`, you can `M-q` which automatically breaks up the line at
column number 80. See `C-h k M-q` for mode-specific information about this
feature.

2025-11-17: I now use the hook `(text-mode . turn-on-auto-fill)` which handles
this automatically in text-mode buffers. See [`gleemacs-languages/text-mode`](#h:9d320186-fbf2-4133-aa52-ca5af7da103d) for
more information and settings.

    (setq-default fill-column 80)


<a id="h:dbdbf8ed-8999-4525-b0f2-a4542de22bb6"></a>

## `which-key` was it again?

This is an extremely useful package that displays the commands available to you based on *which key* you press next. It&rsquo;s particularly helpful as you get accustomed to Emacs, and more generally when you forget the keymap you need once in a blue moon. I find this package most practical when mappings are deeply nested, such as Org&rsquo;s `C-c`.

Eventually these things become second nature and you hardly ever see the display initiate, but like a good friend, it&rsquo;s always there when you need it!

    ;; ; Which Key -------------------
    (use-package which-key
      :ensure nil  ; built in!
      :diminish which-key-mode
      :hook (after-init . which-key-mode)
      :config
      (setq which-key-prefix-prefix "+")
      (setq which-key-idle-delay 1)
      (setq which-key-add-column-padding 2)
      (setq which-key-max-display-columns 4)
      (setq which-key-idle-secondary-delay 0.25))


<a id="h:b24ee109-23e4-4bfb-8b83-99b8e7eba8da"></a>

## Emacs tweaks


<a id="h:c6bcd8f2-1303-4f19-b91d-aafb20f57476"></a>

### Disable lockfiles

For my work flow lock files aren&rsquo;t necessary, so that functionality is disabled here.

    ;; ; Emacs Tweaks -------------------
    ;; disable backup and lock files
    ;; (setq make-backup-files nil)
    ;; (setq backup-inhibited nil) ; Not sure if needed, given `make-backup-files'
    (setq create-lockfiles nil)


<a id="h:9276394b-cbaf-4c3d-b6c2-a1ab11ff1dab"></a>

### `custom.el` be gone!

By default Emacs writes to `init.el` even if you haven&rsquo;t made any changes using `M-x customize` and dirties our configuration files unnecessarily. Therefore we disable the functionality by piping the `custom.el` file to a temporary file.

For users (heathens!!!) who want to use this functionality the relevant settings
are provided in comments below.

    ;; Completely disable `custom.el', thanks Prot!
    ;; If you use `custom.el', you should comment this out:
    (setq custom-file (make-temp-file "emacs-custom-"))
    
    ;; Send custom to `<USER-EMACS-DIR>/custom.el':
    ;; (setq custom-file (expand-file-name "custom.el" user-emacs-directory))
    ;; This just sets up the custom file location and stops emacs from writing
    ;; the crap in `init.el'. To actually utilise the `custom.el', uncomment:
    ;; (when (file-exists-p custom-file)
    ;;   (load custom-file))


<a id="h:7e76e4c7-7110-43aa-99f5-45c73c8ede2f"></a>

## Require gleemacs modules

    ;; ; Add gleemacs module support
    (mapc
     (lambda (string)
       (add-to-list 'load-path (locate-user-emacs-file string)))
     '("gleemacs-modules"))
    
    ;; Now we require more glee...
    (require 'gleemacs-essentials)
    (require 'gleemacs-completion)
    (require 'gleemacs-search)
    (require 'gleemacs-dired)
    (require 'gleemacs-window)
    (require 'gleemacs-git)
    (require 'gleemacs-org)
    (require 'gleemacs-denote)
    (require 'gleemacs-markdown)
    (require 'gleemacs-rss)
    (require 'gleemacs-terminal)
    (require 'gleemacs-languages)
    (require 'gleemacs-eglot)
    (require 'gleemacs-flymake)
    (require 'gleemacs-python)
    (require 'gleemacs-auth)
    (require 'gleemacs-email)
    (require 'gleemacs-irc)
    (require 'gleemacs-spellcheck)
    (require 'gleemacs-keybindings)
    
    ;;; init.el ends here


<a id="h:166c7b83-0b4c-4a99-a99a-f112621ba71e"></a>

# Welcome to the house of glee (*gleemacs* modules)


<a id="h:256acaa3-01eb-4124-90f8-9301afe362f0"></a>

## `gleemacs-auth`

To preserve the privacy of data like email addresses, IRC logins, and other
private information, *gleemacs* makes use of the `auth-source` package. The idea
is to be able to share or publicly store configurations without leaking
sensitive or otherwise private data.

Use the helper function [`gleemacs-helper-auth-get-field` ](#h:be40964e-8203-4630-b1fd-28c505cc25fe)to easily make use of
your `.authinfo.gpg` file as needed in this config.

*[ This function and idea is courtesy of Protesilaos Stavrou. See
<https://protesilaos.com/emacs/dotemacs#h:2fca749c-a84e-415c-9ac0-b1518d06fa51> ]*


<a id="h:c44cf259-09cb-4bcd-aaf0-6751ed32a3f2"></a>

### Header

    ;;; gleemacs-auth.el --- gpg more like gp-Glee! -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; This module expects that you have setup an `.authinfo.gpg' file
    ;; in the correct format.  It's main purpose is to provide a safe
    ;; way for users to store their private emails in public git repos
    ;; without leaking them.
    
    ;;; Code:


<a id="h:e38965aa-74c8-418e-8f79-922efb9bcd04"></a>

### `auth-source`

    (use-package auth-source
      :ensure nil
      :defer t
      :config
      (setq auth-sources '("~/.authinfo.gpg")))


<a id="h:bd322906-bede-42cb-8399-56de650b36b4"></a>

### Set `user-full-name`

    (setq user-full-name "Sam Sinclair")


<a id="h:8897861c-ab39-45a1-a3ef-48f75435d6f8"></a>

### Set `user-email-address`

    (require 'gleemacs-helpers)
    
    ;; ;; Set mail address on notmuch startup
    (add-hook 'notmuch-hello-mode-hook
              (lambda ()
                (let ((email (gleemacs-helper-auth-get-field "public" :user)))
                  (setq user-mail-address email))))
              ;; 100)  ; High priority


<a id="h:65e5d34a-6fba-4756-9d90-14e61113c679"></a>

### Footer

    ;; ; Now providing gpglee...
    (provide 'gleemacs-auth)
    
    ;;; gleemacs-auth.el ends here


<a id="h:980eafe5-4b26-415d-8738-6f7450c0afd2"></a>

## `gleemacs-completion`


<a id="h:e2a47336-d2ed-403b-8811-b4e3bdf6cde7"></a>

### Header

    ;;; gleemacs-completion.el --- Completion toolings for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:85798d37-a2d9-48b7-8e33-f7a14d111d0f"></a>

### `vertico`

    ;; ; Vertico!
    (use-package vertico
      :ensure t
      :hook (after-init . vertico-mode)
      :config
      (setq vertico-scroll-margin 0)
      (setq vertico-resize t)
      (setq vertico-cycle t))


<a id="h:9b6105ed-8ae3-4617-adf4-cb850094e02e"></a>

### `orderless`

`orderless` is a package that provides fuzzy search and is extremely useful,
especially when looking for a particular command, function, or file that you
can&rsquo;t quite remember the name of. For how this is used, see the [minibuffer section](#h:5441ef86-9e1e-4cbd-a5f2-6a3c1f5591d7).

    ;; ; Where we're going, we don't need no orders
    (use-package orderless
      :ensure t
      :config
      ;; Remember to check my `completion-styles' and the
      ;; `completion-category-overrides'.
      (setq orderless-matching-styles '(orderless-prefixes
    				    orderless-regexp))
      (setq orderless-smart-case 1)
      ;; SPC should never complete: use it for `orderless' groups.
      ;; The `?' is a regexp construct.
      :bind ( :map minibuffer-local-completion-map
              ("SPC" . nil)
              ("?" . nil)))


<a id="h:5441ef86-9e1e-4cbd-a5f2-6a3c1f5591d7"></a>

### `minibuffer`

Here we configure our completion styles for the minibuffer. Completion styles
are prioritised in the order they are written, so if a match isn&rsquo;t found by the
first style, the next style is used, until no matches are returned. Where a
`completion-category-overrides` is not set for a category, the default
`completion-styles` will be used.

This took effort to get to the way I like, but it was worth it.

    ;;; Minibuffer completion setup
    ;; Courtesy of Protesilaos Stavrou
    (use-package minibuffer
      :ensure nil
      :config
      (setq completion-styles '(basic orderless))
      ;; (setq completion-category-defaults nil)
      (setq completion-category-overrides
            ;; NOTE 2021-10-25: I am adding basic' because it works better as a
            ;; default for some contexts.  Read:
            ;; <https://debbugs.gnu.org/cgi/bugreport.cgi?bug=50387>.
            ;;
            ;; partial-completion' is a killer app for files, because it
            ;; can expand ~/.l/s/fo to ~/.local/share/fonts.
            ;;
            ;; If basic' cannot match my current input, Emacs tries the
            ;; next completion style in the given order.  In other words,
            ;; orderless' kicks in as soon as I input a space or one of its
            ;; style dispatcher characters.
            '((file (styles . (basic partial-completion orderless)))
              (bookmark (styles . (basic substring)))
              (library (styles . (basic substring)))
              (embark-keybinding (styles . (basic substring)))
              (imenu (styles . (basic substring orderless)))
              (consult-location (styles . (basic substring orderless)))
              (kill-ring (styles . (emacs22 orderless)))
              (eglot (styles . (emacs22 substring orderless))))))
    
    ;; ; Ignore letting casing in minbuffer
    (setq read-buffer-completion-ignore-case t)
    (setq-default case-fold-search t)   ; For general regexp
    (setq read-file-name-completion-ignore-case t)


<a id="h:9d423ab9-41cc-4a31-8479-a2a62b4abd39"></a>

### `dabbrev`

To quote `C-h P dabbrev`:

> The purpose with this package is to let you write just a few
> characters of words you&rsquo;ve written earlier to be able to expand
> them.
> 
> To expand a word, just put the point right after the word and press
> M-/ (dabbrev-expand) or M-C-/ (dabbrev-completion).

Couldn&rsquo;t have put it better myself! Unlike other configs `dabbrev-completion` is
not automatic, as in, you must activate it yourself with `M-C-/`. I prefer this
as it can be distracting and annoying to be constantly suggested abbreviations
that are useless or unwanted.

    ;; ; Dynamic Abbreviation aka dabbrev
    ;;;; `dabbrev' (dynamic word completion (dynamic abbreviations))
    (use-package dabbrev
      :ensure nil
      :commands (dabbrev-expand dabbrev-completion)
      :config
      (setq dabbrev-abbrev-char-regexp "\\sw\\|\\s_")
      (setq dabbrev-abbrev-skip-leading-regexp "[$*/=~']")
      (setq dabbrev-backward-only nil)
      (setq dabbrev-case-distinction 'case-replace)
      (setq dabbrev-case-fold-search nil)
      (setq dabbrev-case-replace 'case-replace)
      (setq dabbrev-check-other-buffers t)
      (setq dabbrev-eliminate-newlines t)
      (setq dabbrev-upcase-means-case-search t)
      (setq dabbrev-ignored-buffer-modes
            '(archive-mode image-mode docview-mode pdf-view-mode)))


<a id="h:5fdf3884-a37d-4335-abc3-452151e99ed8"></a>

### `corfu`

    (use-package corfu
      :ensure t
      :hook (after-init . global-corfu-mode)
      ;; I also have (setq tab-always-indent 'complete) for TAB to complete
      ;; when it does not need to perform an indentation change.
      :bind (:map corfu-map ("<tab>" . corfu-complete))
      :config
      (setq corfu-preview-current nil)
      (setq corfu-min-width 20)
      (setq corfu-popupinfo-delay '(1.25 . 0.5))
      (corfu-popupinfo-mode 1) ; shows documentation after `corfu-popupinfo-delay'
      ;; Sort by input history (no need to modify `corfu-sort-function').
      (with-eval-after-load 'savehist
        (corfu-history-mode 1)
        (add-to-list 'savehist-additional-variables 'corfu-history)))


<a id="h:81d93f7b-a77e-4bb3-b361-71d038d1c561"></a>

### `consult`

    (use-package consult
      :ensure t
      :hook (completion-list-mode . consult-preview-at-point-mode)
      :bind
      ( :map global-map
        ("M-g M-g" . consult-goto-line)
        ("M-s M-b" . consult-buffer)
        ("M-s M-f" . consult-find)
        ("M-s M-g" . consult-grep)
        ("M-s M-h" . consult-history)
        ("M-s M-i" . consult-imenu)
        ("M-s M-l" . consult-line)
        ("M-s M-m" . consult-mark)
        ("M-s M-y" . consult-yank-pop)
        ("M-s M-s" . consult-outline)
        :map consult-narrow-map
        ("?" . consult-narrow-help))
      :init
      ;; Optionally configure the register formatting. This improves the register
      (setq register-preview-delay 0.5
            register-preview-function #'consult-register-format)
      ;; Optionally tweak the register preview window.
      (advice-add #'register-preview :override #'consult-register-window)
      ;; Use Consult to select xref locations with preview
      (setq xref-show-xrefs-function #'consult-xref
            xref-show-definitions-function #'consult-xref)
      :config
      (setq consult-line-numbers-widen t)
      ;; (setq completion-in-region-function #'consult-completion-in-region)
      (setq consult-async-min-input 3)
      (setq consult-async-input-debounce 0.5)
      (setq consult-async-input-throttle 0.8)
      (setq consult-narrow-key nil)
      (setq consult-find-args
            (concat "find . -not ( "
                    "-path */.git* -prune "
                    "-or -path */.cache* -prune )"))
      (setq consult-preview-key 'any)
      (setq consult-project-function nil) ; always work from the current directory (use `cd' to switch directory)
      (add-to-list 'consult-mode-histories '(vc-git-log-edit-mode . log-edit-comment-ring))
      (require 'consult-imenu)) ; the `imenu' extension is in its own file


<a id="h:6b8551e8-f759-4587-9025-9f68108165c1"></a>

### `embark`

    ;; Extended minibuffer actions and more (embark.el)
    (use-package embark
      :ensure t
      :bind
      ( :map minibuffer-local-map
        ("C-c C-c" . embark-collect)
        ("C-c C-e" . embark-export)))


<a id="h:d3069adc-ceae-4c81-8775-badb11120799"></a>

### `embark-consult`

    ;; Needed for correct exporting while using Embark with Consult
    ;; commands.
    (use-package embark-consult
      :ensure t
      :after (embark consult))


<a id="h:7c14d1bf-c821-4d83-b6f9-f528c26e1ddc"></a>

### `marginalia`

    ;;; Detailed completion annotations (marginalia.el)
    (use-package marginalia
      :ensure t
      :commands (marginalia-mode marginalia-cycle)
      :init (marginalia-mode)
      :config
      (setq marginalia-max-relative-age 0)) ; absolute time


<a id="h:c0c9d708-8650-49f3-8d79-65b4397bbcd7"></a>

### Nerd icons for `marginalia`

    ;; Nerd icons for marginalia
    (use-package nerd-icons-completion
      :after marginalia
      :init (nerd-icons-completion-mode))


<a id="h:d4d6c42f-a5f0-4905-b691-98d29216e5bc"></a>

### `yasnippet`

    ;; YASnippet is a template system designed that enhances text editing by
    ;; enabling users to define and use snippets. When a user types a short
    ;; abbreviation, YASnippet automatically expands it into a full template, which
    ;; can include placeholders, fields, and dynamic content.
    ;;
    ;; Courtesy of James Cherti
    (use-package yasnippet
      :ensure t
      :commands (yas-minor-mode
                 yas-global-mode)
      :diminish (yas-minor-mode
    	     yas-global-mode)
      :hook
      (after-init . yas-global-mode)
      :custom
      (yas-also-auto-indent-first-line t)  ; Indent first line of snippet
      (yas-also-indent-empty-lines t)
      (yas-snippet-revival nil)  ; Setting this to t causes issues with undo
      (yas-wrap-around-region nil) ; Do not wrap region when expanding snippets
      ;; (yas-triggers-in-field nil)  ; Disable nested snippet expansion
      ;; (yas-indent-line 'fixed) ; Do not auto-indent snippet content
      ;; (yas-prompt-functions '(yas-no-prompt))  ; No prompt for snippet choices
      :init
      ;; Suppress verbose messages
      (setq yas-verbosity 0))


<a id="h:f9afdabe-ae42-4206-ad49-113ec0c34272"></a>

### `yasnippet-snippets`

    ;; The official collection of snippets for yasnippet.
    (use-package yasnippet-snippets
      :ensure t
      :after yasnippet)
    
    ;; YASnippet is a template system designed that enhances text editing by
    ;; enabling users to define and use snippets. When a user types a short
    ;; abbreviation, YASnippet automatically expands it into a full template, which
    ;; can include placeholders, fields, and dynamic content.
    ;;
    ;; Courtesy of James Cherti
    (use-package yasnippet
      :ensure t
      :commands (yas-minor-mode
                 yas-global-mode)
      :diminish (yas-minor-mode
    	     yas-global-mode)
      :hook
      (after-init . yas-global-mode)
      :custom
      (yas-also-auto-indent-first-line t)  ; Indent first line of snippet
      (yas-also-indent-empty-lines t)
      (yas-snippet-revival nil)  ; Setting this to t causes issues with undo
      (yas-wrap-around-region nil) ; Do not wrap region when expanding snippets
      ;; (yas-triggers-in-field nil)  ; Disable nested snippet expansion
      ;; (yas-indent-line 'fixed) ; Do not auto-indent snippet content
      ;; (yas-prompt-functions '(yas-no-prompt))  ; No prompt for snippet choices
      :init
      ;; Suppress verbose messages
      (setq yas-verbosity 0))


<a id="h:58c6ea8f-8cbb-419e-870f-6e7d74091d84"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-completion)
    
    ;;; gleemacs-completion.el ends here


<a id="h:f0b6e819-48c4-426f-ac6b-d47c0a235e7b"></a>

## `gleemacs-denote`


<a id="h:803a2d06-e3a3-465d-b407-b3964fac17c8"></a>

### Header

    ;;; gleemacs-denote.el --- Denote setup for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; Simply the best implementation of plain text note taking.
    
    ;;; Code:
    
    ;; Remember that the website version of this manual shows the latest
    ;; developments, which may not be available in the package you are
    ;; using.  Instead of copying from the web site, refer to the version
    ;; of the documentation that comes with your package.  Evaluate:
    ;;
    ;;     (info "(denote) Sample configuration")


<a id="h:1e06e325-83ea-4ce6-bf24-32bfdb751769"></a>

### `denote`

    ;; ; Denote!
    (use-package denote
      :ensure t
      :hook
      ( ;; If you use Markdown or plain text files, then you want to make
       ;; the Denote links clickable (Org renders links as buttons right
       ;; away)
       (text-mode . denote-fontify-links-mode-maybe)
       ;; Apply colours to Denote names in Dired.  This applies to all
       ;; directories.  Check `denote-dired-directories' for the specific
       ;; directories you may prefer instead.  Then, instead of
       ;; `denote-dired-mode', use `denote-dired-mode-in-directories'.
       (dired-mode . denote-dired-mode))
      :bind
      ;; Denote DOES NOT define any key bindings.  This is for the user to
      ;; decide.  For example:
      ;; ( :map global-map
      ;;   ("C-c n n" . denote)
      ;;   ("C-c n d" . denote-dired)
      ;;   ("C-c n g" . denote-grep)
      ;;   ;; If you intend to use Denote with a variety of file types, it is
      ;;   ;; easier to bind the link-related commands to the `global-map', as
      ;;   ;; shown here.  Otherwise follow the same pattern for `org-mode-map',
      ;;   ;; `markdown-mode-map', and/or `text-mode-map'.
      ;;   ("C-c n l" . denote-link)
      ;;   ("C-c n L" . denote-add-links)
      ;;   ("C-c n b" . denote-backlinks)
      ;;   ("C-c n q c" . denote-query-contents-link) ; create link that triggers a grep
      ;;   ("C-c n q f" . denote-query-filenames-link) ; create link that triggers a dired
      ;;   ;; Note that `denote-rename-file' can work from any context, not just
      ;;   ;; Dired bufffers.  That is why we bind it here to the `global-map'.
      ;;   ("C-c n r" . denote-rename-file)
      ;;   ("C-c n R" . denote-rename-file-using-front-matter)
    
        ;; Key bindings specifically for Dired.
       ( :map dired-mode-map
        ("C-c C-d C-i" . denote-dired-link-marked-notes)
        ("C-c C-d C-r" . denote-dired-rename-files)
        ("C-c C-d C-k" . denote-dired-rename-marked-files-with-keywords)
        ("C-c C-d C-R" . denote-dired-rename-marked-files-using-front-matter))
    
      :config
      ;; Remember to check the doc string of each of those variables.
      (setq denote-directory (expand-file-name "~/org/"))
      (setq denote-save-buffers nil)
      (setq denote-known-keywords '("emacs"))
      (setq denote-infer-keywords t)
      (setq denote-sort-keywords t)
      (setq denote-prompts '(title keywords))
      (setq denote-excluded-directories-regexp nil)
      (setq denote-keywords-to-not-infer-regexp nil)
      (setq denote-rename-confirmations '(rewrite-front-matter modify-file-name))
    
      ;; Pick dates, where relevant, with Org's advanced interface:
      (setq denote-date-prompt-use-org-read-date t)
    
      ;; Automatically rename Denote buffers using the `denote-rename-buffer-format'.
      (denote-rename-buffer-mode 1))


<a id="h:871bbef8-ae1e-4862-89b1-bd10236d40d6"></a>

### `denote-journal`

    ;; ; A journal a day keeps the doctor away
    (use-package denote-journal
      :ensure t
      :after denote
      ;; Bind those to some key for your convenience.
      :commands ( denote-journal-new-entry
                  denote-journal-new-or-existing-entry
                  denote-journal-link-or-create-entry )
      ;; :bind
      :hook (calendar-mode . denote-journal-calendar-mode)
      :config
      ;; Use the "journal" subdirectory of the `denote-directory'.  Set this
      ;; to nil to use the `denote-directory' instead.
      (setq denote-journal-directory
            (expand-file-name "journal" denote-directory))
      ;; Default keyword for new journal entries. It can also be a list of
      ;; strings.
      (setq denote-journal-keyword "journal")
      ;; Read the doc string of `denote-journal-title-format'.
      (setq denote-journal-title-format 'day-date-month-year))


<a id="h:2afb941f-4e89-4b0c-bbef-569e89296457"></a>

### Footer

    ;; ; Now providing gleenote...
    
    (provide 'gleemacs-denote)
    
    ;;; gleemacs-denote.el ends here


<a id="h:ecd9dbed-0146-4d05-a49f-7688fe89e20d"></a>

## `gleemacs-dired`


<a id="h:7a7e9e1b-b255-4929-a9db-f6adc9714e95"></a>

### Header

    ;;; gleemacs-dired.el --- Dired config for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:c91fd2c6-4293-4a88-bb82-32e246381e56"></a>

### `dired`

    ;; ; Dired
    (use-package dired
      :ensure nil
      :commands (dired)
      :config
      (setq dired-recursive-copies 'always)
      (setq dired-recursive-deletes 'always)
      (setq delete-by-moving-to-trash t)
      (setq dired-listing-switches
            "-AGFhlv --group-directories-first --time-style=long-iso")
      ;; Constrain vertical cursor movement to lines within the buffer
      (setq dired-movement-style 'bounded-files)
      (add-hook 'after-init-hook #'window-divider-mode)
      ;; Stop direds "Omitting..." noise clogging up `*Messages*'
      (setq dired-omit-verbose nil)
      (add-hook 'dired-mode-hook #'dired-omit-mode)
      (add-hook 'dired-mode-hook #'hl-line-mode)
      (add-hook 'dired-mode-hook #'diff-hl-dired-mode)
      (setq dired-auto-revert-buffer #'dired-directory-changed-p)
      (setq dired-make-directory-clickable t)
      (setq dired-free-space nil)
      (setq dired-dwim-target t))


<a id="h:d0980651-f735-47b5-83b1-9babeb6f2efa"></a>

### `dired-subtree`

    ;; This let's us `<TAB>' to expand a directory and list it's nested
    ;; contents as a subtree.
    (use-package dired-subtree
      :ensure t
      :after dired
      :bind
      ( :map dired-mode-map
        ("<tab>" . dired-subtree-toggle)
        ("TAB" . dired-subtree-toggle)
        ("<backtab>" . dired-subtree-remove)
        ("S-TAB" . dired-subtree-remove))
      :config
      (setq dired-subtree-use-backgrounds nil))


<a id="h:f8205753-6e96-44f9-8bd4-d0424fd45b99"></a>

### Nerd icons for `dired`

    ;; ; Prettyyyyyyyy
    (use-package nerd-icons-dired
      :hook
      (dired-mode . nerd-icons-dired-mode)
      :diminish nerd-icons-dired-mode)


<a id="h:329aa092-fe8d-4c6a-8393-05dfab9969e5"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-dired)
    
    ;;; gleemacs-dired.el ends here


<a id="h:364049fb-8890-4987-82ad-9eb83a775d99"></a>

## `gleemacs-eglot`


<a id="h:df497911-70b1-4420-aee7-a4292f3c068b"></a>

### Header

    ;;; gleemacs-eglot.el --- Eglot setup for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:471c68b9-6dd0-4a59-b0cc-5235221d4650"></a>

### `eglot` and `basedpyright`

    ;; Set up the Language Server Protocol (LSP) servers using Eglot.
    (use-package eglot
      :hook ((python-mode python-ts-mode) . eglot-ensure)
      :config
      (setq eglot-autoshutdown 1)
      (add-to-list 'eglot-server-programs
                   '((python-mode python-ts-mode)
                     . ("basedpyright-langserver" "--stdio")))
      (setq-default eglot-workspace-configuration
                    '(:basedpyright (:typeCheckingMode "recommended"
                                         :reportMissingImports t
                                         :reportUnusedVariable t
                                         :venvPath ".venv"
                                         :venv ".venv"
                                         :pythonPath "bin/python"))))


<a id="h:1beed37e-a196-409f-8072-746142b48414"></a>

### `consult-eglot`

    (use-package consult-eglot
      :after eglot)


<a id="h:99e9fea9-cb8f-4a24-89bf-2d62b99d7247"></a>

### `eldoc`

    ;; Setup eldoc
    (use-package eldoc
      :ensure nil
      :hook ((eglot-managed-mode . eldoc-mode))
      :diminish eldoc-mode
      :custom
      (eldoc-echo-area-use-multiline-p 2)
      (eldoc-idle-delay 3.0)
      :config
      (with-eval-after-load 'eldoc-box
        (diminish 'eldoc-box-hover-at-point-mode)))


<a id="h:96144615-3be1-4cca-99ae-d7bc28296237"></a>

### `eldoc-box`

    ;; Setup eldoc in-frame popups
    (use-package eldoc-box
      :ensure t
      :after eglot
      :hook (eglot-managed-mode . eldoc-box-hover-at-point-mode)
      :custom
      ;; tweak delay before popup
      (eldoc-box-idle-delay 2)
      ;; move popups above the cursor for readability
      (eldoc-box-hover-display-frame-above-point t)
      ;; customise hide borders
      (eldoc-box-clear-frame-parameters '((internal-border-width . 6)
                                          (left-fringe . 8)
                                          (right-fringe . 8))))


<a id="h:cb207868-3b28-40d3-998e-642bdd4981c3"></a>

### Taming `eglot` hints

    ;; uncomment this if hints become too noisy
    ;; (setq eglot-ignored-server-capabilities '(:inlayHintProvider))
    (setq eglot-send-changes-idle-time 0.3)


<a id="h:3cb7e4b6-79c3-4969-98a3-3e772ec20b47"></a>

### Footer

    ;; ; Now providing gleeglot...
    (provide 'gleemacs-eglot)
    
    ;;; gleemacs-eglot.el ends here


<a id="h:56e960b9-260e-4224-a0c3-4ca5089a5288"></a>

## `gleemacs-email`


<a id="h:fe4b44b9-130d-4abd-aa96-d0fdfd11b0e8"></a>

### Header

    ;;; gleemacs-email.el --- Gleemail -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:9761fcad-8f24-4203-bfc0-47d6800629c0"></a>

### `message`

    (use-package message
      :ensure nil
      :defer t
      :hook
      (message-setup . message-sort-headers)
      :config
      (setq mail-user-agent 'message-user-agent
            message-mail-user-agent t) ; use `mail-user-agent'
      (setq mail-header-separator "--text follows this line--")
      (setq message-elide-ellipsis "\n> [... %l lines elided]\n")
      (setq compose-mail-user-agent-warnings nil)
      (setq message-citation-line-function #'message-insert-formatted-citation-line)
      (setq message-citation-line-format (concat "> From: %f\n"
                                                 "> Date: %a, %e %b %Y %T %z\n"
                                                 ">")
            message-ignored-cited-headers "") ; default is "." for all headers
      (setq message-confirm-send t)
      (setq message-kill-buffer-on-exit t)
      ;; (add-to-list 'mm-body-charset-encoding-alist '(utf-8 . base64))
      (setq message-wide-reply-confirm-recipients nil))


<a id="h:d5fc5720-4999-4022-bd3b-010d6ac25160"></a>

### `smtpmail`

    (use-package smtpmail
      :ensure nil
      :after message
      :config
      ;; Load gnutls library and add local cert to trustfiles
      (require 'gnutls)
      (add-to-list 'gnutls-trustfiles (expand-file-name "~/.cert/cert.pem"))
      (setq send-mail-function #'smtpmail-send-it)
      (setq smtpmail-smtp-server "127.0.0.1")
      (setq smtpmail-smtp-service 1025)
      (setq smtpmail-stream-type 'starttls))


<a id="h:fe79d830-af9b-4208-8e22-143180fdabaf"></a>

### `notmuch`

    (require 'gleemacs-helpers)
    
    (use-package notmuch
      :ensure t
      :defer t
      :commands (notmuch notmuch-mua-new-mail notmuch-hello-mode)
      :config
      (let ((private (gleemacs-helper-auth-get-field "private" :user))
    	(public  (gleemacs-helper-auth-get-field "public" :user)))
        (setq notmuch-identities
    	  (mapcar (lambda (str)
    		    (format "%s <%s>" user-full-name str))
    		  (list private public))
    	  notmuch-fcc-dirs
    	  `((,private . "private/Sent")
    	    (,public . "public/Sent"))))
      (setq notmuch-tree-unthreaded t)
      (setq notmuch-search-oldest-first nil)
      (setq notmuch-saved-searches
    	'((:name "inbox"
    		 :query "tag:inbox"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "i")
    	  (:name "unread"
    		 :query "tag:unread"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "u")
    	  (:name "flagged"
    		 :query "tag:flagged"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "f")
    	  (:name "sent"
    		 :query "tag:replied"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "r")
    	  (:name "drafts"
    		 :query "tag:draft"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "d")
    	  (:name "all mail"
    		 :query "*"
    		 :sort-order newest-first
    		 :search-type unthreaded
    		 :key "a")))
      ;; Remove certain emails from inbox
      (setq notmuch-message-replied-tags '("+replied" "-inbox"))
      (setq notmuch-message-forwarded-tags '("+forwarded" "-inbox"))
      (setq notmuch-draft-tags '("+draft" "-inbox")))


<a id="h:efe915b0-87ec-451f-8e33-1a714484c96e"></a>

### Footer

    ;; ; Now providing gleemail...
    (provide 'gleemacs-email)
    
    ;;; gleemacs-email.el ends here


<a id="h:0f9e3288-97a6-434e-80b4-ebc231ef68a1"></a>

## `gleemacs-essentials`


<a id="h:3138aad9-2507-48b6-8833-75a2347b21f2"></a>

### Header

    ;;; gleemacs-essentials.el --- Essentials for Glee! -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; The essentials are designed to be a base sit of modifications
    ;; and packages that aim to provide sane defaults for persistency
    ;; and practical aesthetics.
    
    ;;; Code:


<a id="h:d4fa3323-709f-48da-87b8-b1091167a07e"></a>

### `emacs` settings

    ;;;; `emacs' essential configuration
    ;; Courtesy of Protesilaos Stavrou
    (use-package emacs
      :ensure nil
      :demand t
      :config
      ;; General settings and common custom functions
      (setq blink-matching-paren nil)
      (setq custom-unlispify-tag-names nil)
      (setq delete-pair-blink-delay 0.1) ; Emacs28
      (setq delete-pair-push-mark t) ; Emacs 31
      (setq echo-keystrokes-help nil) ; Emacs 30
      (setq epa-keys-select-method 'minibuffer) ; Emacs 30
      (setq eval-expression-print-length nil)
      (setq find-library-include-other-files nil) ; Emacs 29
      (setq help-window-select t)
      (setq kill-do-not-save-duplicates t)
      (setq mode-require-final-newline 'visit-save)
      (setq next-error-recenter '(4)) ; center of the window
      (setq remote-file-name-inhibit-auto-save t)                 ; Emacs 30
      (setq remote-file-name-inhibit-delete-by-moving-to-trash t) ; Emacs 30
      (setq save-interprogram-paste-before-kill t)
      (setq scroll-error-top-bottom t)
      (setq tramp-connection-timeout (* 60 10)) ; seconds
      (setq truncate-partial-width-windows nil)
      ;; emacs asks confirm before exiting
      (setq confirm-kill-emacs 'y-or-n-p))


<a id="h:633f6502-cf8a-4b33-9420-fd07ce8f43b3"></a>

### `diminish`

    ;;;; `diminish'
    ;; Would you mind not being so loud down there?!
    (use-package diminish
      :config
      (diminish 'visual-line-mode))


<a id="h:26522f14-b8f6-43d5-b422-dc07a49e8aa8"></a>

### `recentf`

Maintains a list of recently opened files. Convenient when you need to jump back
in later!

    ;;;; Recentf Config
    (use-package recentf
      :ensure nil
      :hook (after-init . recentf-mode)
      :config
      (setq recentf-max-menu-items 1000)
      (setq recentf-max-saved-items 100))


<a id="h:1f755079-5ac9-44a8-a6ec-d2d4e67c4c1d"></a>

### `savehist`

    ;;;; `savehist' (minibuffer and related histories)
    (use-package savehist
      :ensure nil
      :hook (after-init . savehist-mode)
      :config
      (setq savehist-file (expand-file-name "savehist" no-littering-var-directory))
      (setq history-length 100)
      (setq history-delete-duplicates t)
      (setq savehist-save-minibuffer-history t)
      (dolist (gleemacs-savehist-vars '(kill-ring
    				    mark-ring global-mark-ring
    				    search-ring regexp-search-ring))
      (add-to-list 'savehist-additional-variables gleemacs-savehist-vars)))


<a id="h:aad225b9-a2f8-43e7-8720-e36ed5c6cca8"></a>

### `save-place`

    ;;;; This helped me find my keys once!
    (use-package save-place
      :ensure nil
      :hook (after-init . save-place-mode)
      :config
      (setq save-place-file (expand-file-name "save-place" no-littering-var-directory)))


<a id="h:eea0d09b-94fb-470a-b842-6c6cd231f936"></a>

### `mouse`

    ;;;; Mouse and mouse wheel behaviour
    (use-package mouse
      :ensure nil
      :hook (after-init . mouse-wheel-mode)
      :config
      (setq mouse-autoselect-window t) ; complements the auto-selection of my tiling window manager
      (setq focus-follows-mouse t)
      ;; In Emacs 27+, use Control + mouse wheel to scale text.
      (setq mouse-wheel-scroll-amount
            '(1
              ((shift) . 5)
              ((meta) . 0.5)
              ((control) . text-scale))
            mouse-drag-copy-region nil
            make-pointer-invisible t
            mouse-wheel-progressive-speed t
            mouse-wheel-follow-mouse t)
      ;; Scrolling behaviour
      (setq scroll-preserve-screen-position t
            scroll-conservatively 1 ; affects `scroll-step'
            scroll-margin 0
            next-screen-context-lines 0))


<a id="h:56bef50e-b68e-4511-9b2f-ee91f22b80d2"></a>

### `autorevert`

    ;; ; Automatically update buffers when modified in the background
    ;;;; Auto revert mode
    (use-package autorevert
      :ensure nil
      :hook (after-init . global-auto-revert-mode)
      :config
      (setq auto-revert-verbose t))


<a id="h:d724e6d3-5b33-410d-b4f5-82bf5ebbdac9"></a>

### `delsel`

    ;;;; Delete selection
    (use-package delsel
      :ensure nil
      :hook (after-init . delete-selection-mode))


<a id="h:1244202f-0ad5-4298-b820-296c9d567a79"></a>

### `tooltip`

    ;;;; Tooltips (tooltip-mode)
    (use-package tooltip
      :ensure nil
      :hook (after-init . tooltip-mode)
      :config
      (setq tooltip-delay 0.5
            tooltip-short-delay 0.5
            tooltip-frame-parameters
            '((name . "tooltip")
              (internal-border-width . 10)
              (border-width . 0)
              (no-special-glyphs . t))))


<a id="h:a3b250bb-e279-442a-b9e1-41e3f1972414"></a>

### `no-littering`

This nifty package redirects persistent data to `/var/` and package
configurations to `/etc/`, nested in the `<user-emacs-directory>`. Where
packages require disk useage, they (should) have been configured to utilise the
`no-littering-var-directory` or `no-littering-etc-directory` as necessary.

In addition to cleanliness this should also help to ensure that our
configuration is portable across systems, while minimising the chances of
exposing sensitive data.

    ;;;; `no-literring'
    ;; ; Cleaning up those emacs streets
    ;; A great package the redirects package configuration files and persitent
    ;; data to the emacs directory's /etc and /var folders.
    (use-package no-littering
      :ensure t
      :config
      ;; Prevent recentf junk
      (with-eval-after-load 'recentf
        (add-to-list 'recentf-exclude
                     (recentf-expand-file-name no-littering-var-directory))
        (add-to-list 'recentf-exclude
                     (recentf-expand-file-name no-littering-etc-directory))))


<a id="h:7b619f6f-276e-426e-b0c5-f31aa2258965"></a>

### Send backup files to `no-littering`

Persistence requires writing data to disk, and by default Emacs thinks any
working directory is it&rsquo;s oyster, leading to a lot of stray `#files#` and
`other-files~`, and a cluttered `.emacs.d` folder. To keep our files tidy,
organised, and safe, we send these files to the respective `no-littering-var`
directory.

    (let ((backup-dir (no-littering-expand-var-file-name "backups/"))
          (autosave-dir (no-littering-expand-var-file-name "autosave/")))
      ;; Ensure directories exist
      (make-directory backup-dir t)
      (make-directory autosave-dir t)
    
      ;; Enable backups
      (setq make-backup-files t)
    
      ;; Redirect all backups for `foo.bar~'
      (setq backup-directory-alist `(("." . ,backup-dir)))
    
      ;; Numbered backups
      (setq version-control t
            kept-new-versions 10
            kept-old-versions 2
            delete-old-versions t)
    
      ;; Redirect auto-save files `#foo.bar#'
      (setq auto-save-file-name-transforms
            `((".*" ,(concat autosave-dir "\\1") t)))
    
      ;; Redirect auto-save lists `.saves-*'
      (setq auto-save-list-file-prefix
            (no-littering-expand-var-file-name "autosave/saves-")))


<a id="h:d25b714c-8454-4dea-a2fc-688c5ed22bf7"></a>

### `undo-fu`

    ;; ; Undo fu and session persistence
    ;; The undo-fu package is a lightweight wrapper around Emacs' built-in undo
    ;; system, providing more convenient undo/redo functionality.
    (use-package undo-fu
      :ensure t
      :commands (undo-fu-only-undo
                 undo-fu-only-redo
                 undo-fu-only-redo-all
                 undo-fu-disable-checkpoint))


<a id="h:42d4c972-a186-478f-8459-e6b845e6428a"></a>

### `undo-fu-session`

    ;; The undo-fu-session package complements undo-fu by enabling the saving
    ;; and restoration of undo history across Emacs sessions, even after restarting.
    (use-package undo-fu-session
      :ensure t
      :commands undo-fu-session-global-mode
      :hook (after-init . undo-fu-session-global-mode)
      :custom
      (undo-fu-session-directory
       (expand-file-name "undo-fu/" no-littering-var-directory))
      (undo-fu-session-linear t))


<a id="h:26e3a7a8-2d2e-460e-a571-7c27e157ea0d"></a>

### `server`

    ;;;; Emacs `server' (allow `emacsclient' to connect to running session)
    ;; ; Enable server mode, but only once!
    (use-package server
      :ensure nil
      :defer 1
      :config
      (setq server-client-instructions nil)
      (unless (or (server-running-p) (daemonp))
        (server-start)))


<a id="h:38ec5c6b-dc2e-4255-8573-7803d72209bc"></a>

### `keyboard-quit` DWIM

    ;; DWIM C-g
    ;; Courtesy of Protesilaos
    (defun prot/keyboard-quit-dwim ()
      "Do-What-I-Mean behaviour for a general `keyboard-quit'.
    
      The generic `keyboard-quit' does not do the expected thing when
      the minibuffer is open.  Whereas we want it to close the
      minibuffer, even without explicitly focusing it.
    
      The DWIM behaviour of this command is as follows:
    
      - When the region is active, disable it.
      - When a minibuffer is open, but not focused, close the minibuffer.
      - When the Completions buffer is selected, close it.
      - In every other case use the regular `keyboard-quit'."
      (interactive)
      (cond
       ((region-active-p)
        (keyboard-quit))
       ((derived-mode-p 'completion-list-mode)
        (delete-completion-window))
       ((> (minibuffer-depth) 0)
        (abort-recursive-edit))
       (t
        (keyboard-quit))))
    
    (global-set-key [remap keyboard-quit] 'prot/keyboard-quit-dwim)


<a id="h:76f10d20-34fb-4cf0-ad71-b97a8748c155"></a>

### `nerd-icons`

    (use-package nerd-icons
      :defer 1
      :custom
      (setq nerd-icons-scale-factor 1.1)
      ;; The Nerd Font you want to use in GUI
      ;; "Symbols Nerd Font Mono" is the default and is recommended
      ;; but you can use any other Nerd Font if you want
      ;; (nerd-icons-font-family "Symbols Nerd Font Mono")
      )


<a id="h:8d333d93-c176-47eb-bfbd-28b2474b0b4a"></a>

### `dashboard`

    ;; ; Simple dashboard
    ;; I rarely use the scratch, so lets add some utility at startup!
    (use-package dashboard
      :ensure t
      :config
      (setq dashboard-projects-backend 'project-el)
      (setq dashboard-items '((recents   . 5)
                              (projects  . 5)
                              (bookmarks . 5)))
                              ;; (registers . 5)))
      (setq dashboard-buffer-name "Dashboard")
      (setq dashboard-startupify-list '(dashboard-insert-newline
    				    dashboard-insert-banner
    				    dashboard-insert-newline
    				    dashboard-insert-banner-title
    				    dashboard-insert-newline
    				    dashboard-insert-items
    				    dashboard-insert-init-info
    				    dashboard-insert-newline
    				    dashboard-insert-footer))
      (dashboard-setup-startup-hook))
    
    (setq initial-buffer-choice (lambda () (get-buffer-create dashboard-buffer-name)))


<a id="h:3e5b5870-9fcf-4148-9fe4-4ff49f8eb440"></a>

### `ibuffer` improvements

    ;; ; IBuffer niceties
    ;; This setup courtesy of Steve Purcell
    ;; https://github.com/purcell/emacs.d/blob/master/lisp/init-ibuffer.el
    ;; In short, when we C-x C-b our IBuffer display is grouped by project
    (use-package ibuffer-vc
      :ensure t
      :hook (ibuffer . ibuffer-set-up-preferred-filters)
      :init
      (defun ibuffer-set-up-preferred-filters ()
        (ibuffer-vc-set-filter-groups-by-vc-root)
        (unless (eq ibuffer-sorting-mode 'filename/process)
          (ibuffer-do-sort-by-filename/process)))
      :config
      (setq-default ibuffer-show-empty-filter-groups nil)
      (setq ibuffer-filter-group-name-face 'font-lock-doc-face)
      (setq ibuffer-formats
            '((mark modified read-only vc-status-mini " "
    		(icon 2 2 :left)
                    (name 22 22 :left :elide)
                    " "
                    (size-h 9 -1 :right)
                    " "
                    (mode 12 12 :left :elide)
                    " "
                    vc-relative-file)
              (mark modified read-only vc-status-mini " "
    		(icon 2 2 :left)
                    (name 22 22 :left :elide)
                    " "
                    (size-h 9 -1 :right)
                    " "
                    (mode 14 14 :left :elide)
                    " "
                    (vc-status 12 12 :left)
                    " "
                    vc-relative-file)))
    
      ;; after ibuffer loads
      (with-eval-after-load 'ibuffer
        (define-ibuffer-column size-h
          (:name "Size" :inline t)
          (file-size-human-readable (buffer-size)))))


<a id="h:39010b7a-776c-49e9-8f54-25655514a601"></a>

### Replace `list-buffers` with `ibuffer`

    (global-set-key [remap list-buffers] 'ibuffer)


<a id="h:1caab0d9-f479-4276-904e-0622027768b7"></a>

### Nerd icons for `ibuffer`

    ;; ; ibuffer nerd-icons
    ;; Thanks to Prot for mentioning this one. Icons are extremely useful for
    ;; differentiating buffers when you have metric tonnes of them open.
    (use-package nerd-icons-ibuffer
      :ensure t
      :defer t
      :hook (ibuffer-mode . nerd-icons-ibuffer-mode)
      :config
      (setq nerd-icons-ibuffer-icon t))


<a id="h:a5894071-9977-44d8-8262-13a4d9a6a466"></a>

### Footer

    ;; Now providing the gleessentials!
    (provide 'gleemacs-essentials)
    
    ;;; gleemacs-essentials.el ends here


<a id="h:a10f4b83-b0b2-4306-9a0e-a21790378a9c"></a>

## `gleemacs-flymake`


<a id="h:d6b0d7f6-6317-49df-8e85-1d12094b352c"></a>

### Header

    ;;; gleemacs-flymake.el --- Flymake Goodness! -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:e093d306-a762-464d-9785-28160030990e"></a>

### `flymake`

    ;;;; `flymake'
    (use-package flymake
      :ensure t
      :hook (prog-mode . flymake-mode)
      :config
      (setq flymake-suppress-zero-counters t))
    
    (defun gleemacs/flymake-eldoc-setup ()
      (add-hook 'eldoc-documentation-functions
                #'flymake-eldoc-function
                nil t))


<a id="h:b3d33660-fbfd-44d8-a787-5c1d4bcd9a20"></a>

### `flymake-flycheck`

    ;;;; `flycheck'
    (use-package flymake-flycheck
      :after flymake
      :hook ((flymake-mode-hook . flymake-flycheck.auto)
    	 (prog-mode-hook . flymake-mode)
             (flymake-mode . gleemacs/flymake-eldoc-setup)))


<a id="h:688d447a-1237-4fc4-a8d8-f507593be547"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-flymake)
    
    ;;; gleemacs-flymake.el ends here


<a id="h:cfd83654-5a5a-4fcb-a73c-873ee94c640f"></a>

## `gleemacs-git`


<a id="h:e04fc654-76e0-43b8-abd6-6f8b86534365"></a>

### Header

    ;;; gleemacs-git.el --- Git and Projects for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:2598412a-c086-427f-b907-d3cac8ec7abc"></a>

### `project`

    ;; ; Projects Setup
    ;;;; `project'
    (use-package project
      :ensure nil
      :bind
      (("C-x p ." . project-dired)
       ("C-x p C-g" . keyboard-quit)
       ("C-x p <return>" . project-dired)
       ("C-x p <delete>" . project-forget-project))
      :config
      (setopt project-switch-commands
              '((project-find-file "Find file")
                (project-find-regexp "Find regexp")
                (project-find-dir "Find directory")
                (project-dired "Root dired")
                (project-vc-dir "VC-Dir")
                (project-shell "Shell")
                (keyboard-quit "Quit")))
      (setq project-vc-extra-root-markers '(".project")) ; Emacs 29
      (setq project-key-prompt-style t)) ; Emacs 30


<a id="h:33f332b5-0e61-40fe-8149-fafbfdbd5be8"></a>

### `transient`

    (use-package transient
      :defer t
      :config
      (setq transient-show-popup 0.5))


<a id="h:7b29aa9e-dbbf-4529-a877-4b2f60fa3263"></a>

### `magit`

    ;;; Interactive and powerful git front-end (Magit)
    (use-package magit
      :ensure t
      :bind
      ( :map global-map
        ("C-c g g" . magit-status)
        :map magit-mode-map
        ("C-w" . nil)
        ("M-w" . nil))
      :init
      (setq magit-define-global-key-bindings nil)
      ;; (setq magit-section-visibility-indicator '(magit-fringe-bitmap . magit-fringe-bitmap))
      :config
      (setq git-commit-summary-max-length 50)
      ;; NOTE 2023-01-24: I used to also include `overlong-summary-line'
      ;; in this list, but I realised I do not need it.  My summaries are
      ;; always in check.  When I exceed the limit, it is for a good
      ;; reason.
      (setq git-commit-style-convention-checks '(non-empty-second-line))
    
      (setq magit-diff-refine-hunk t)
    
      ;; Show icons for files in the Magit status and other buffers.
      (with-eval-after-load 'magit
        (setq magit-format-file-function #'magit-format-file-nerd-icons)))


<a id="h:14dafaa6-f211-4915-acf0-e896ff8fbe9a"></a>

### `magit-repos`

    (use-package magit-repos
      :ensure nil ; part of `magit'
      :commands (magit-list-repositories)
      :init
      (setq magit-repository-directories
            '(("~/GitHub/" . 2)))
      ;; Make escape quit magit prompts
      :config (define-key transient-map (kbd "<escape>") 'transient-quit-one))


<a id="h:4decf0f8-2f1d-429c-9f5f-01e7d9b796b5"></a>

### `diff-hl`

    ;; Diff-hl
    (use-package diff-hl
      :hook ((dired-mode         . diff-hl-dired-mode-unless-remote)
             (magit-post-refresh . diff-hl-magit-post-refresh))
      :init (global-diff-hl-mode))


<a id="h:4734c810-5628-4980-a4e0-95959622cdc4"></a>

### Footer

    ;; ; Now providing gleet..
    (provide 'gleemacs-git)
    
    ;;; gleemacs-git.el ends here


<a id="h:636cea02-f3c5-4a3c-8ad6-7107ffda3c14"></a>

## `gleemacs-helpers`


<a id="h:ad02ef8f-955f-4bb3-89e4-552bcfa993f3"></a>

### Header

    ;;; gleemacs-helpers.el --- Friendly Helpers -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;;;
    ;;; Commentary:
    ;;
    ;; Just a bunch of helpful helpers gleefully helping.
    ;;
    ;;;
    ;;; Code:


<a id="h:be40964e-8203-4630-b1fd-28c505cc25fe"></a>

### `gleemacs-helper-auth-get-field`

    ;; This useful function is courtesy of Protesilaos Stavrou, and allows for
    ;; secure retrieval of key-value pairs from `.authinfo.gpg' files.
    ;; See: https://protesilaos.com/emacs/dotemacs#h:24f17614-ee3d-4cd1-bbe3-f53e4f39c281
    ;; Useage: email (gleemacs-helper-auth-get-field "public" :user)
    ;;        (setq user-mail-address email)
    ;;;###autoload
    (defun gleemacs-helper-auth-get-field (host prop)
      "Find PROP in `auth-sources' for HOST entry."
      (require 'auth-source)
      (when-let* ((source (auth-source-search :host host)))
        (if (eq prop :secret)
            (funcall (plist-get (car source) prop))
          (plist-get (flatten-list source) prop))))


<a id="h:66df97ea-6162-4df2-9942-f143fa66bfd6"></a>

### Footer

    ;; ; Now providing gleeful helpers...
    (provide 'gleemacs-helpers)
    
    ;;; gleemacs-helpers.el ends here


<a id="h:1ee51d4d-54c1-463f-859c-80291e000f36"></a>

## `gleemacs-irc`


<a id="h:5e8b7974-a1cc-4981-b7e1-1dc3a5d621cf"></a>

### Header

    ;;; gleemacs-irc.el --- Gleemacs IRC -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; sTfU oR pEoN
    
    ;;; Code:


<a id="h:12b5a267-5dfe-408e-a3d2-9ab2024695d6"></a>

### `erc` setup

    ;;;; `erc'
    (use-package erc
      :ensure nil
      :config
      (setq erc-track-exclude-types '("JOIN" "PART" "QUIT" "NICK" "MODE"))
      (setq erc-prompt-for-nickserv-password nil
            erc-user-full-name "Sam Sinclair"
            erc-use-tls t)
      (setq erc-autojoin-channels-alist
            '(("Libera.Chat" "#emacs" "#fsf" "#linux" "#linux-aus" "#archlinux" "#archlinux-aur")))	
      )


<a id="h:01947a1a-509f-4e8f-815f-e9c38200b0e3"></a>

### `erc-libera-connect`

    (require 'gleemacs-helpers)
    
    ;; See `gleemacs-keybindings' for usage
    (defun gleemacs/erc-libera-connect ()
      "Connect to Libera.Chat using ERC and authinfo credentials."
      (interactive)
      (let ((nick (gleemacs-helper-auth-get-field "irc.libera.chat" :user)))
        (erc-tls :server "irc.libera.chat"
                 :port 6697
                 :nick nick)))


<a id="h:e8cea086-9796-44b1-8eab-eec63fd426fb"></a>

### Footer

    (provide 'gleemacs-irc)
    
    ;;; gleemacs-irc.el ends here


<a id="h:28d03a5b-c2d1-47f1-9bcb-0eabaf390d21"></a>

## `gleemacs-keybindings`


<a id="h:fb8b5aa9-3c2b-498d-bffa-13b3fdba5c22"></a>

### Header

    ;;; gleemacs-keybindings.el --- Gleemacs Keybindings -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; A centralised place to organise your bindings.
    
    ;;; Code:


<a id="h:5f1e71cc-5a01-4b5a-9c40-c8e87b69b125"></a>

### override and adjust `emacs` defaults

    ;;; ; Emacs Defaults
    ;; Keys I unbind here are either to avoid accidents or to bind them
    ;; elsewhere later in the configuration.
    (use-package emacs
      :bind
      ( :map global-map
        ("C-z" . nil) ; I have a window manager, thanks!
        ("C-x C-z" . nil) ; same idea as above
        ("C-x C-c" . nil) ; avoid accidentally exiting Emacs
        ("C-x C-r" . recentf-open) ; override `find-file-read-only'
        ("C-h h" . nil) ; Never show that "hello" file
        ("M-`" . nil)
        ("C-h K" . describe-keymap) ; overrides `Info-goto-emacs-key-command-node'
        ("C-h u" . apropos-user-option)
        ("C-h F" . apropos-function) ; lower case is `describe-function'
        ("C-h V" . apropos-variable) ; lower case is `describe-variable'
        ("C-h L" . apropos-library) ; lower case is `view-lossage'
        ("C-h c" . describe-char))) ; overrides `describe-key-briefly'


<a id="h:e7094933-cc3e-460b-8f08-65c988d62843"></a>

### `org`

    ;;; ; Org Mode niceties
    (use-package org
      :bind
      ( :map org-mode-map
        ("C-M-<return>" . org-insert-subheading)
        ("M-S-<return>" . org-insert-todo-subheading)))


<a id="h:bbf7582f-15aa-4dfb-8abe-365a56d1686e"></a>

### `general`

Utilising a centralised module for our bindings effectively presents an
interface to our workspace in one area. Therefore, we always know where to look
to get a birds-eye view of our mappings. This approach (in theory) also minimises
error in terms of overwriting existing bindings, which can be easy to do when
they&rsquo;re spread around. The downside being a duplication of efforts in removing
packages and their bindings (if any) from the aforementioned module, but this
shouldn&rsquo;t happen often.

My reasoning for using `general` was a matter of speed of deployment and ease of
configuration in the outset, and because leader keys have bosses too. I
understand this adds unnecessary bloat (as it turns out, [`general` is not just
for mapping bindings](https://github.com/noctuid/general.el?tab=readme-ov-file#making-the-most-of-general), salute!), so I&rsquo;d like to roll my own functionality later.

    ;;; ; AttennnnnnnNTION!
    (use-package general
      :ensure t
      :config
      ;; Define the leader key
      (general-create-definer my/leader
        :prefix "C-c")
    
      ;; Global bindings
      (my/leader
        ;; Reserving this for flymake and eglot
        ;; "c"  '(:ignore t :which-key "code")
        
        
        "f"  '(:ignore t :which-key "files")
        "ff" '(find-file :which-key "find file")
        "fr" '(recentf-open-files :which-key "recent files")
    
        "b"  '(:ignore t :which-key "buffers")
        "bb" '(switch-to-buffer :which-key "switch buffer")
        "bk" '(kill-buffer :which-key "kill buffer")
    
        ;; Insert
        "i"  '(:ignore t :which-key "insert")
        "is" '(clipboard-kill-ring-save :which-key "save to clipboard")
        "ip" '(mouse-yank-primary :which-key "yank clipboard pop")
    
        ;; Open
        "o"  '(:ignore t :which-key "open")
        "oe" '(notmuch :which-key "email")
        "oc" '(gleemacs/erc-libera-connect :which-key "erc")
        "or" '(elfeed :which-key "elfeed")
        "ot" '(vterm :which-key "vterm")
    
        ;; ; Notes
        "n"  '(:ignore t :which-key "notes")
        "na" '(org-agenda :which-key "org-agenda")
        "nb" '(denote-backlinks :whick-key "denote-backlinks")
        "nn" '(denote :which-key "denote-create-note")
        "no" '(denote-open-or-create :which-key "denote-find-notes")
        "nf" '(denote-grep :which-key "denote-grep")
        "nr" '(denote-dired :which-key "denote-regex")
        "nj" '(denote-journal-new-entry :which-key "denote-journal")
        "nl" '(denote-link-or-create :which-key "denote-insert-link")
        "nL" '(denote-add-links :which-key "denote-insert-links")
        "nx" '(org-capture :which-key "org-capture")
        "nr" '(denote-rename-file :which-key "denote rename note")
        "nR" '(denote-rename-file-using-front-matter "denote rename w front matter")
        "ns" '(org-search-view :which-key "org-search-notes")
        "nt" '(org-todo-list :which-key "todo list")
    
        ;; search
        "s"  '(:ignore t :which-key "search")
        "sb" '(consult-line :which-key "buffer")
        "sb" '(consult-line-multi 'all-buffers :which-key "all buffers")
        "sd" '(dictionary-search :which-key "dictionary-search")
        
    
        "w"  '(:ignore t :which-key "windows")
        "we" '(balance-windows :which-key "balance windows")
        "wm" '(maximize-window :which-key "maximise window")
        "wd" '(delete-window :which-key "delete window")
    
        "g"  '(:ignore t :which-key "git")
        "gg" '(magit-status :which-key "status")
        "gc" '(magit-commit :which-key "commit")
    
        "C-q"  '(save-buffers-kill-terminal :which-key "quit emacs")))


<a id="h:02a18d18-174c-4c93-b823-20be30b25b4f"></a>

### Footer

    ;; ; Now providing gleebindings...
    (provide 'gleemacs-keybindings)
    
    ;;; gleemacs-keybindings.el ends here


<a id="h:3aa88b4e-bc43-4601-87f7-4d873b682284"></a>

## `gleemacs-markdown`


<a id="h:e44aef34-2462-4821-a3d8-9841c1774fa4"></a>

### Header

    ;;; gleemacs-markdown.el --- Markdown in gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:424d0663-3631-4c7c-a15e-e8e606248ac0"></a>

### `markdown-mode`

    (use-package markdown-mode
      :ensure t
      :mode ("\\.md\\'" . markdown-mode)
      :init
      (setq markdown-command "pandoc"))


<a id="h:5352989a-d87e-4a37-a966-e3b74443c94a"></a>

### `markdown-toc`

    (use-package markdown-toc
      :after markdown-mode
      :commands (markdown-toc-generate-toc markdown-toc-refresh-toc))


<a id="h:10e8198c-9171-40e0-886a-41c862ef6f2b"></a>

### Footer

    ;;; Now providing glee...
    (provide 'gleemacs-markdown)
    
    ;;; gleemacs-markdown.el ends here


<a id="h:e7ecab49-b5dc-4a79-8c7b-ea34283bbc03"></a>

## `gleemacs-languages`


<a id="h:3b22c03b-99b7-4345-a51a-60b4df54c80b"></a>

### Header

    ;;; gleemacs-org.el --- Langauges in gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:453aea7d-dc31-4d29-b0f9-1abef1ac9d16"></a>

### `treesit`

    ;; Setup our grammar sources list
    (setq treesit-language-source-alist
          '((python "https://github.com/tree-sitter/tree-sitter-python")
            (c "https://github.com/tree-sitter/tree-sitter-c")
            (bash "https://github.com/tree-sitter/tree-sitter-bash")
            (json "https://github.com/tree-sitter/tree-sitter-json")
    	(html "https://github.com/tree-sitter/tree-sitter-html")
    	(css "https://github.com/tree-sitter/tree-sitter-css")	
            (toml "https://github.com/tree-sitter/tree-sitter-toml")
    	(make "https://github.com/tree-sitter-grammars/tree-sitter-make")))
    
    ;; Map major modes to a treesit mode 
    (setq major-mode-remap-alist
          '(;(python-mode . python-ts-mode)
            (css-mode . css-ts-mode)
            (bash-mode . bash-ts-mode)
            (json-mode . json-ts-mode)
    	(sh-mode . bash-ts-mode)))


<a id="h:9d320186-fbf2-4133-aa52-ca5af7da103d"></a>

### `text-mode`

These settings are also inherited by other `text-mode` modes such as `org` and `markdown`.

    (use-package text-mode
      :ensure nil
      :mode "\\`\\(README\\|CHANGELOG\\|COPYING\\|LICENSE\\)\\'"
      :hook
      ((text-mode . turn-on-auto-fill)
       (prog-mode . (lambda () (setq-local sentence-end-double-space t))))
      :config
      (setq sentence-end-double-space nil)
      (setq sentence-end-without-period nil)
      (setq colon-double-space nil)
      (setq use-hard-newlines nil)
      (setq adaptive-fill-mode t))


<a id="h:fcb18d03-aa56-421e-a162-47b127c27f59"></a>

### Settings for common file types


<a id="h:f9f334ba-ab90-4781-bc31-4e674a194d5d"></a>

#### `PKGBUILD`

    ;;;; Arch Linux packaging scripts (sh-mode)
    (use-package sh-script
      :ensure nil
      :mode ("PKGBUILD" . sh-mode))


<a id="h:092260fc-c4ec-412d-b9db-6f42c2eff2e0"></a>

#### `systemd` and `.conf` files

    ;;;; SystemD and other configuration files (conf-mode)
    (use-package conf-mode
      :ensure nil
      :mode ("\\`dircolors\\'" "\\.\\(service\\|timer\\)\\'"))


<a id="h:1cb7c234-5a1d-4dd5-a057-9ccb08ff4b94"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-languages)
    
    ;;; gleemacs-org.el ends here


<a id="h:6653a561-f152-4d5f-83b2-fb5281d9de84"></a>

## `gleemacs-org`


<a id="h:5439ad83-a951-4788-881b-9b0847cd9bf4"></a>

### Header

    ;;; gleemacs-org.el --- Org for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:4ef90aa0-40f0-4704-8c3a-94a5e8779835"></a>

### `australia-holidays`

    ;; ; Set up calendar
    ;; Straya holidays c/o jmibanez
    (use-package australia-holidays
      :ensure t)


<a id="h:6e5f1be3-c0f4-4a27-ae66-9e18a5d4d3df"></a>

#### Add daylight savings time

    (with-eval-after-load 'australia-holidays
      (setq australia-holidays-for-vic
            (append australia-holidays-for-vic
                    '((holiday-float 10 0 1 "Daylight Savings starts (forward 1 hour @ 02:00)")
                      (holiday-float 4 0 1 "Daylight Savings ends (back 1 hour @ 03:00)")))))


<a id="h:9b1bb859-a811-46f8-afaa-d13a9ae9f337"></a>

### `calendar`

    (use-package calendar
      :ensure nil
      :commands (calendar)
      :config
      (setq calendar-mark-diary-entries-flag nil)
      (setq calendar-mark-holidays-flag t)
      (setq calendar-mode-line-format nil)
      (setq calendar-time-display-form
            '( 24-hours ":" minutes
               (when time-zone (format "(%s)" time-zone))))
      (setq calendar-week-start-day 1)      ; Monday
      (setq calendar-date-style 'iso)
      (setq calendar-time-zone-style 'numeric) ; Emacs 28.1
      (setq calendar-holidays (append australia-holidays-for-vic))
      (require 'cal-dst)
      (setq calendar-standard-time-zone-name "+1000")
      (setq calendar-daylight-time-zone-name "+1100"))


<a id="h:8605aa5c-86d0-49fe-8d9e-a3cb90213f5c"></a>

### `org`

    ;; ; Org Mode
    ;; Organised Relatively Gracefully
    (use-package org
      :ensure nil
      :init
      (setq org-directory (expand-file-name "~/org/"))
      (setq org-default-notes-file (expand-file-name "notes.org" org-directory))
      (setq org-agenda-files
    	'("notes.org"
    	  "projects.org"
    	  "todo.org"))
      (setq org-imenu-depth 7)
      (add-to-list 'safe-local-variable-values '(org-hide-leading-stars . t))
      (add-to-list 'safe-local-variable-values '(org-hide-macro-markers . t))


<a id="h:a3b098a1-ea22-4385-b44b-b3d19c23ac2b"></a>

#### Org general settings

    :config
    ;;;; general settings
    (setq org-ellipsis " [...]")
    (setq org-M-RET-may-split-line '((default . nil)))
    (setq org-hide-emphasis-markers nil)
    (setq org-hide-leading-stars nil)
    (setq org-cycle-separator-lines 0)
    (setq org-fold-catch-invisible-edits 'show)
    (setq org-loop-over-headlines-in-active-region 'start-level)
    (setq org-read-date-prefer-future 'time)
    (setq org-highlight-latex-and-related nil) ; other options affect elisp regexp in src blocks
    (setq org-fontify-quote-and-verse-blocks t)
    (setq org-fontify-whole-block-delimiter-line t)
    (setq org-track-ordered-property-with-tag t)
    (setq org-highest-priority ?A)
    (setq org-lowest-priority ?C)
    (setq org-default-priority ?A)
    (setq org-startup-indented t)
    ;; No blank lines before new entries
    (setq org-blank-before-new-entry
          '((heading . nil)
            (plain-list-item . nil)))


<a id="h:7df0c93a-20be-4e4c-b72a-8f758ec41d45"></a>

#### Org indentation settings

    ;; Indentation settings
    (setq org-insert-heading-respect-content t)
    (setq org-adapt-indentation nil)
    (setq org-indentation-per-level 4)


<a id="h:8492d68e-b711-4204-91bf-ba99d4fb9408"></a>

#### Org todo and refile settings

    ;; Todo and Refile settings
    ;; The evil do when I do todos
    (setq org-todo-keywords
          '((sequence "TODO(t)" "MAYBE(m)" "|" "DONE(d!)" "CANCELED(c@)")))
    (setq org-refile-targets
          '((org-agenda-files :maxlevel . 3)
            (my/org-files-list :maxlevel . 3)
            (nil :maxlevel . 3)))
    (setq org-refile-use-outline-path 'file
          org-outline-path-complete-in-steps nil
          org-refile-allow-creating-parent-nodes 'confirm)
    ;; Time and State Logging
    (setq org-log-done 'time)
    (setq org-log-into-drawer t)
    (setq org-log-note-clock-out nil)
    (setq org-log-redeadline 'time)
    (setq org-log-reschedule 'time)


<a id="h:47c08a20-0133-4565-a3cc-d69febae1c3c"></a>

#### Org links

    ;; Links
    (setq org-return-follows-link t)
    (setq org-link-context-for-files t)
    (setq org-link-keep-stored-after-insertion nil)
    (setq org-id-link-to-org-use-id 'create-if-interactive-and-no-custom-id)


<a id="h:2016204b-69ee-46ba-a5dd-cdb08c8ef460"></a>

#### Org codeblock settings

    ;; Codeblocks
    (setq org-confirm-babel-evaluate nil)
    (setq org-src-window-setup 'current-window)
    (setq org-edit-src-persistent-message nil)
    (setq org-src-fontify-natively t)
    (setq org-src-preserve-indentation t)
    (setq org-src-tab-acts-natively t)
    (setq org-edit-src-content-indentation 0)


<a id="h:f7156605-dbbc-40d2-abff-396b13bc962e"></a>

#### Org export settings

    ;; Export
    (setq org-export-with-toc t)
    (setq org-export-headline-levels 8)
    (setq org-export-dispatch-use-expert-ui nil)
    (setq org-html-htmlize-output-type nil)
    (setq org-html-head-include-default-style nil)
    (setq org-html-head-include-scripts nil)


<a id="h:c22df481-ccb9-4e19-94ab-e6b2c0c6f9b1"></a>

#### Setup project-based note taking

      ;; project helpers
      (defun my/project-name ()
        "Return current project name or error."
        (let* ((proj (project-current))
               (root (and proj (project-root proj))))
          (if root
              (file-name-nondirectory (directory-file-name root))
            (user-error "Not in a project"))))
    
      ;; central target helper
      (defun my/org--central-file (file project)
        "Visit FILE under `org-directory` and ensure PROJECT tree exists.
    Leaves point at the subtree and returns the current buffer."
        (let ((path (expand-file-name file org-directory)))
          (set-buffer (org-capture-target-buffer path))
          (widen)
          (goto-char (point-min))
          (my/org--ensure-heading
           (delq nil
                 (append (org-capture-get :parents)
                         (list project (org-capture-get :heading)))))
          (current-buffer)))
    
      ;; wrappers for org-capture
      (defun my/org-capture-central-project-todo-target ()
        (my/org--central-file "projects.org" (my/project-name)))
    
      (defun my/org-capture-central-project-notes-target ()
        (my/org--central-file "projects.org" (my/project-name)))
    
      (defun my/org-capture-central-project-changelog-target ()
        (my/org--central-file "projects.org" (my/project-name)))
    
      ;; Project-aware Org capture templates
      (defvar my/org-capture-todo-file "todo.org")
      (defvar my/org-capture-notes-file "notes.org")
      (defvar my/org-capture-changelog-file "changelog.org")
      (defvar my/org-capture-projects-file "projects.org")
    
      (defun my/project-root ()
        ;;   "Return the current project root or signal an error."
        (or (and (fboundp 'project-root)
                 (ignore-errors (project-root)))
            (and (fboundp 'project-current)
                 (when-let ((proj (project-current))) (project-root proj)))
            (user-error "Not in a project")))
    
      (defun my/org--local-root (filename)
        ;;   "Find FILENAME in the nearest parent directory or project root."
        (let ((path (locate-dominating-file default-directory filename)))
          (expand-file-name filename (or path (my/project-root)))))
    
      (defun my/org-capture-project-todo-file ()
        (my/org--local-root my/org-capture-todo-file))
    
      (defun my/org-capture-project-notes-file ()
        (my/org--local-root my/org-capture-notes-file))
    
      (defun my/org-capture-project-changelog-file ()
        (my/org--local-root my/org-capture-changelog-file))
    
      (defun my/org--ensure-heading (headings &optional level)
        "Ensure nested HEADINGS exist up to LEVEL in the current buffer."
        (setq level (or level 1))
        (if (not headings)
            (widen)
          (if (and (re-search-forward
                    (format org-complex-heading-regexp-format
                            (regexp-quote (car headings))) nil t)
                   (= (org-current-level) level))
              (progn (beginning-of-line) (org-narrow-to-subtree))
            (goto-char (point-max))
            (unless (bolp) (insert "\n"))
            (insert (make-string level ?*) " " (car headings) "\n")
            (beginning-of-line 0))
          (my/org--ensure-heading (cdr headings) (1+ level))))


<a id="h:4dd2e73f-d6aa-4e9f-8edd-23a627c4afa5"></a>

#### Setup capture templates

    ;; Personal
    (setq org-capture-templates
          `(("t" "Personal todo" entry
             (file+headline ,(expand-file-name "todo.org" org-directory) "Inbox")
             ,(concat "* TODO %?\n%i"
                      ":PROPERTIES:\n"
                      ":CAPTURED: %U\n"
                      ":CUSTOM_ID: h:%(format-time-string \"%Y%m%dT%H%M%S\")\n"
                      ":END:\n\n"
                      "%a")
             :empty-lines-after 1
             :prepend t)
            ("n" "Personal note" entry
             (file+headline ,(expand-file-name "notes.org" org-directory) "Inbox")
             ,(concat "* %u %?\n%i"
                      ":PROPERTIES:\n"
                      ":CAPTURED: %U\n"
                      ":CUSTOM_ID: h:%(format-time-string \"%Y%m%dT%H%M%S\")\n"
                      ":END:\n\n"
                      "%a")
             :empty-lines-after 1
             :prepend t)
            ("j" "Journal" entry
             (file+olp+datetree ,(expand-file-name "journal.org" org-directory))
             ,(concat "* %U %?\n%i"
                      ":PROPERTIES:\n"
                      ":CAPTURED: %U\n"
                      ":CUSTOM_ID: h:%(format-time-string \"%Y%m%dT%H%M%S\")\n"
                      ":END:\n\n"
                      "%a")
             :empty-lines-after 1
             :prepend t)
            ;; Project Specific Templates
            ("p" "Templates for projects")
            ;; 
            ("pt" "Project-local todo" entry    ; {project-root}/todo.org
             (file+headline (my/org-capture-project-todo-file) "Inbox")
             "* TODO %?\n%i\n%a" :prepend t)
            
            ("pn" "Project-local notes" entry   ; {project-root}/notes.org
             (file+headline (my/org-capture-project-notes-file) "Inbox")
             "* %U %?\n%i\n%a" :prepend t)
            
            ("pc" "Project-local changelog" entry ; {project-root}/changelog.org
             (file+headline (my/org-capture-project-changelog-file) "Unreleased")
             "* %U %?\n%i\n%a" :prepend t)
            
            ;; ;; Centralise Project Templates
            ("o" "Centralized project")
            ("ot" "Project todo" entry
             (function my/org-capture-central-project-todo-target)
             "* TODO %?\n%U\n%i\n%a"
             :heading "Tasks")
            ("on" "Project notes" entry
             (function my/org-capture-central-project-notes-target)
             "* %U %?\n%i\n%a"
             :heading "Notes" :prepend t)
            ("oc" "Project changelog" entry
             (function my/org-capture-central-project-changelog-target)
             "* %U %?\n%i\n%a"
             :heading "Changelog" :prepend t))))


<a id="h:5044085c-0a6a-4ad7-ab22-69c5109ef035"></a>

#### Custom function `gleemacs/org-assign-custom-ids`

    (defun gleemacs/org-assign-custom-ids ()
      "Assign CUSTOM_ID to all Org headings in the current buffer that lack one.
    IDs formatted as h:<UUID>."
      (interactive)
      (org-map-entries
       (lambda ()
         (unless (org-entry-get nil "CUSTOM_ID")
           (let ((id (concat "h:" (org-id-new))))
             (org-entry-put nil "CUSTOM_ID" id))))))


<a id="h:4b2fd9db-9373-4ce1-86b7-b9a801882337"></a>

#### 


<a id="h:739682b4-1f1e-43df-8f1d-711957de87d3"></a>

### `org-superstar`

    ;; Org Superstar
    ;; Make headings and lists nice :)
    (use-package org-superstar
      :ensure t
      :after org
      :hook (org-mode . org-superstar-mode)
      :config
      ;; Set different bullets, with one getting a terminal fallback.
      (setq org-superstar-headline-bullets-list
          '("◉" ("🞛" ?◈) "○" "▷"))
      ;; Stop cycling bullets to emphasize hierarchy of headlines.
      (setq org-superstar-cycle-headline-bullets nil)
      ;; Hide away leading stars on terminal.
      (setq org-superstar-leading-fallback ?\s))


<a id="h:8741adc1-c6df-4d29-9b23-abacf218470e"></a>

### `org-tempo`

    ;; Org Tempo
    ;; Allows expansion of `<s' + TAB to expand a begin_src tag
    (use-package org-tempo
      :ensure nil
      :after org)


<a id="h:69843e13-a6f8-4c84-991a-4002ebed33f9"></a>

### `ox-gfm`

    ;; `ox-gfm'
    ;; GitHub flavoured markdown exporting for org
    (use-package ox-gfm
      :ensure t
      :after org)


<a id="h:e58983a7-0f63-4e77-86b0-ec1834060ef9"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-org)
    
    ;;; gleemacs-org.el ends here


<a id="h:be7c601e-e790-44c6-aa3c-33f2dc720995"></a>

## `gleemacs-python`


<a id="h:e7e68f1c-45d9-46ff-9d87-35632f2f5463"></a>

### Header

    ;;; gleemacs-python.el --- Gleefull Python -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:210cd552-be3e-4e7c-98f6-511c6ffeca64"></a>

### General settings

    ;; I appreciate the guess, but do it quietly please :)
    ;; Silence guessing indent messages!
    (setq python-indent-guess-indent-offset-verbose nil)


<a id="h:cb877ca4-c55d-497f-b2e7-bb2c005eda36"></a>

### `pyvenv`

    (use-package pyvenv
      :ensure t
      :hook ((python-mode python-ts-mode) . my/pyvenv-auto)
      :config
      (defun my/pyvenv-auto ()
        "Auto-activate project .venv if present."
        (let ((venv (locate-dominating-file default-directory ".venv")))
          (when venv
            (pyvenv-activate (expand-file-name ".venv" venv))))))


<a id="h:f61fec5d-8c14-4f12-a865-912311d75560"></a>

### Footer

    (provide 'gleemacs-python)
    
    ;;; gleemacs-python.el ends here


<a id="h:993722af-6bc3-4f03-a95d-f1135c1de22d"></a>

## `gleemacs-rss`


<a id="h:a41cad18-44bd-4ca0-bbb8-9c08420ac147"></a>

### Header

    ;;; gleemacs-rss.el --- RSS for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;; Gleerss are on the house!
    
    ;;; Code:


<a id="h:314d3429-ad83-4c3a-a15e-87f1d0ece6e8"></a>

### `elfeed`

    ;; Elfeed
    ;; Get your favourite writings and other tidibits in plain text
    (use-package elfeed
      :ensure t
      :hook
      ((elfeed-show-mode . visual-line-mode)
       (elfeed-search-mode . elfeed-update))
      :commands elfeed
      :init
      (setq elfeed-db-directory
    	(expand-file-name "elfeed/db" no-littering-var-directory)
        	elfeed-enclosure-default-dir
    	(expand-file-name "elfeed/enclosures" no-littering-var-directory))
      :config
      (setq elfeed-search-filter "@2-weeks-ago")
      (setq elfeed-feeds
            '("https://lwn.net/headlines/rss"
    	  "https://sachachua.com/blog/feed/index.xml"
              "https://protesilaos.com/master.xml"
    	  "https://suckless.org/atom.xml"))
    
      (make-directory elfeed-db-directory t))


<a id="h:5737ed1b-3140-4856-b308-a49f08741ffb"></a>

### `elfeed-goodies` setup

    (use-package elfeed-goodies
      :after elfeed
      :config
      (elfeed-goodies/setup))


<a id="h:412b5eb6-272a-4e21-af9a-00c9c5f88516"></a>

### Footer

    ;; ; Now providing the glee...
    (provide 'gleemacs-rss)
    
    ;;; gleemacs-rss.el ends here


<a id="h:8c4a6980-dc81-4432-b1f9-c9be2dda56ec"></a>

## `gleemacs-search`


<a id="h:52f06824-fb5f-45e8-a062-1c6fea118493"></a>

### Header

    ;;; gleemacs-search.el --- Search setup for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:b77b8d4c-0656-493e-8f10-d613730c5268"></a>

### `isearch`

    ;; ; `isearch'
    ;; Like the phone, but much better
    (use-package isearch
      :ensure nil
      :demand t
      :config
      ;; shows the position of current match releative to total count.
      (setq isearch-lazy-count t)
      (setq lazy-count-prefix-format "(%s/%s) ")
      (setq lazy-count-suffix-format nil))


<a id="h:f4a774ca-b1ee-47fc-a4ba-0f526ebc13ba"></a>

### `rg` and `ripgrep` tooling

    ;;; grep and xref tooling
    ;; Courtesy of Protesilaos
    (defvar gleemacs/ripgrep (or (executable-find "rg") (executable-find "ripgrep"))
      "Store path to ripgrep executable, else nil.")


<a id="h:9e7c4a55-8045-4e6d-9720-5eb2bbb35b68"></a>

### `re-builder`

    (use-package re-builder
      :ensure nil
      :commands (re-builder regexp-builder)
      :config
      (setq reb-re-syntax 'read))


<a id="h:15401141-af3c-4a32-8028-8b0d43f8ab3e"></a>

### `xref`

    (use-package xref
      :ensure nil
      :commands (xref-find-definitions xref-go-back)
      :config
      ;; All those have been changed for Emacs 28
      (setq xref-show-definitions-function #'xref-show-definitions-completing-read) ; for M-.
      (setq xref-show-xrefs-function #'xref-show-definitions-buffer) ; for grep and the like
      (setq xref-file-name-display 'project-relative)
      (setq xref-search-program (if gleemacs/ripgrep 'ripgrep 'grep)))


<a id="h:a15faa9b-f6a8-4916-a2a0-85d946904a3c"></a>

### `grep`

    (use-package grep
      :ensure nil
      :commands (grep lgrep rgrep)
      :config
      (setq grep-save-buffers nil)
      (setq grep-use-headings t) ; Emacs 30
    
      (setq grep-program (or gleemacs/ripgrep (executable-find "grep")))
      (setq grep-template
            (if gleemacs/ripgrep
                "/usr/bin/rg -nH --null -e <R> <F>"
              "/usr/bin/grep <X> <C> -nH --null -e <R> <F>")))


<a id="h:56e9dc83-b519-46dc-8dbd-c6b21375a8b2"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-search)
    
    ;;; gleemacs-search.el ends here


<a id="h:236323c2-3e7f-49bf-8605-71ed41347ab3"></a>

## `gleemacs-spellcheck`


<a id="h:32dd0b7f-6dbd-4790-8f7e-aaae7faf4e55"></a>

### Header

    ;;; gleemacs-spellcheck.el --- Spellcheck for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:32041c31-7071-49ea-864d-674f67636932"></a>

### `flyspell`

    ;; ; spel chek fr emacs
    (use-package flyspell
      :ensure nil
      :config
      (setq flyspell-issue-message-flag nil)
      (setq flyspell-issue-welcome-flag nil)
      (setq ispell-local-dictionary "en_GB")
      (setq ispell-dictionary "en_GB"))


<a id="h:8a648d54-a04b-41fc-b4c7-9e29b21ed9f5"></a>

### `dictionary`

    ;; ; 8==D tionary
    (use-package dictionary
      :ensure nil
      :config
      (setq dictionary-server "dict.org"
            dictionary-default-popup-strategy "lev" ; read doc string
            dictionary-create-buttons nil
            dictionary-use-single-buffer t))


<a id="h:65abd4c7-6306-4a9e-b97f-75f2e5542865"></a>

### `altcaps`

    ;; ; cOdInG iS dEaD bRo!1!
    ;; RTFM: <https://protesilaos.com/emacs/altcaps>.
    ;; "ALTCAPS Lets Trolls Convert Aphorisms to Proper Shitposts."
    (use-package altcaps
      :ensure t)


<a id="h:99fc4262-588b-4994-b171-2c627842d727"></a>

### Footer

    ;; ; now provyding gle
    (provide 'gleemacs-spellcheck)
    
    ;;; gleemacs-spellcheck.el ends here


<a id="h:2f3dd6c6-cf61-47e5-81fe-fd4dca219cb3"></a>

## `gleemacs-terminal`


<a id="h:47d08db5-09c1-46c7-90c2-a13ece256098"></a>

### Header

    ;;; gleemacs-terminal.el --- terminal? in gleemacs?! -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:4464d571-3f13-4a38-997e-27e07adbbcaf"></a>

### `vterm`

    ;; ; vterm! the C based terminal emulator for emacs
    ;; https://github.com/akermu/emacs-libvterm
    (use-package vterm
      :ensure t)


<a id="h:aaf600ce-8b63-448e-858e-1e2d4fc6e58e"></a>

### Footer

    ;; Now providing gleetty...
    (provide 'gleemacs-terminal)
    
    ;;; gleemacs-terminal.el ends here


<a id="h:768f0eef-b96c-421a-be30-d77fa862661c"></a>

## `gleemacs-window`


<a id="h:1ffef3fa-9036-41bd-a28e-809b8c0d4eda"></a>

### Header

    ;;; gleemacs-window.el --- Window and buffer setup for gleemacs -*- no-byte-compile: t; no-native-compile: t; lexical-binding: t; -*-
    ;; Author: Sam Sinclair
    ;; URL: https://github.com/s6muel/gleemacs
    ;; Package-Requires: ((emacs "29.1"))
    ;; Version: 0.1.0
    ;; SPDX-License-Identifier: GPL-3.0-or-later
    
    ;;; Commentary:
    
    ;;; Code:


<a id="h:5d16cd30-eb31-4b1e-a95b-3a027e319e91"></a>

### Setting up where certain buffers appear

*Taming buffer the magic dragon.*

This is a way to make sure certain buffers are displayed in a way that doesn&rsquo;t inhibit our workspace. Thanks to Prot and his [Emacs video on the subject](https://www.youtube.com/watch?v=1-UIzYPn38s).

    ;; Anatomy of a buffer alist entry
    ( BUFFER-MATCHER  ; The buffer name/type
      LIST-OF-DISPLAY-FUNCTIONS  ; What we want to do with the buffer
      &optional PARAMETERS)

    (setq display-buffer-alist
          '(("\\*Occur\\*"
             (display-buffer-in-direction)
             (direction . below)
             (window-height . 0.3))
    
            ("\\`\\*Async Shell Command\\*\\'"
             (display-buffer-no-window))
    
            ("\\`\\*\\(Warnings\\|Compile-Log\\|Org Links\\)\\*\\'"
             (display-buffer-no-window)
             (allow-no-window . t))
    
            ("\\*\\(Org \\(Select\\|Note\\)\\|Agenda Commands\\)\\*"
             (display-buffer-in-side-window)
             (dedicated . t)
             (side . bottom)
             (slot . 0)
             (window-parameters . ((mode-line-format . none))))
    
            ((or . ((derived-mode . flymake-diagnostics-buffer-mode)
                    (derived-mode . flymake-project-diagnostics-mode)
                    (derived-mode . messages-buffer-mode)
                    (derived-mode . backtrace-mode)))
             (display-buffer-reuse-mode-window display-buffer-at-bottom)
             (mode . (flymake-diagnostics-buffer-mode
                      flymake-project-diagnostics-mode
                      messages-buffer-mode
                      backtrace-mode))
             (window-height . 0.3)
             (dedicated . t)
             (preserve-size . (t . t))
             (body-function . select-window))))


<a id="h:5b641c02-9718-4dc6-be20-86bc7c8e96b9"></a>

### *gleemacs* modeline setup

    ;; ; Setup modeline helpers -----------------
    ;; Right align helper
    (defun gleemacs/mode-line-rhs (segments)
      "Align SEGMENTS to the right."
      (let* ((txt (string-trim (format-mode-line segments)))
             (w   (max 1 (string-width txt))))
        (list
         (propertize " " 'display `((space :align-to (- right ,w))))
         txt)))
    
    ;; Show a path for the buffer instead of just `buffer-file-name'
    (defun gleemacs/mode-line-path ()
      "Return a readable path for the current buffer."
      (cond
       ((buffer-file-name)
        (if-let* ((proj (project-current nil))
                  (root (project-root proj)))
            ;; Inside project: path relative to project root
            (file-relative-name
    	 (propertize buffer-file-name 'face 'bold)
    	root)
          ;; Outside project: ~/full/path
          (abbreviate-file-name
           (propertize buffer-file-name 'face 'bold))))
       ;; Buffers like `*scratch*', `*Messages*' display as is
       (t (propertize
           (format "%s" (buffer-name))
           'face 'bold))))
    
    ;; Project name
    (defun gleemacs/mode-line-project-name ()
      "Return the current project name for the mode line, or empty string."
      (if-let ((proj (ignore-errors (project-current nil))))
          (concat " [" (file-name-nondirectory
                       (directory-file-name (project-root proj))) "] ")
        ""))
    
    ;; VC branch
    (defun gleemacs/mode-line-vc-branch ()
      "Return the current VC branch name with fancy prefix, or empty string."
      (if vc-mode
          (let* ((branch (substring-no-properties vc-mode)))
            (setq branch (string-trim branch))
            ;; Format "Git-master" as " master"
            (setq branch (replace-regexp-in-string "^[A-Za-z]+[-: ]" "" branch))
            (concat "   " branch "  "))
        ""))
    
    (defun gleemacs/terminal-mode-p ()
      "Return non-nil if the current buffer is a terminal.
    
    Covers:
      - vterm
      - term
      - eshell"
      (or
       ;; vterm: real pty
       (eq major-mode 'vterm-mode)
    
       ;; term-mode (ansi-term / term): real pty
       (eq major-mode 'term-mode)
    
       ;; eshell: non-pty but shell-like
       (eq major-mode 'eshell-mode)))
    
    ;; Major mode
    ;; Courtesy of Protesilaos Stavrou
    (defun gleemacs-modeline-major-mode-indicator ()
      "Return appropriate propertised mode line indicator for the major mode."
      (let ((indicator (cond
    		    ((gleemacs/terminal-mode-p) ">_")
                        ((derived-mode-p 'prog-mode) "λ")
    		    ((derived-mode-p 'text-mode) "§")
                        ((derived-mode-p 'comint-mode) ">_")
                        ;; ((derived-mode-p 'vterm-mode) ">_")
                        (t "◦"))))
        (propertize indicator 'face 'shadow)))
    
    ;; `mode-line-format' ---------------
    ;; This configures how the modeline displays. It's basically the default
    ;; with some subtle improvements for `vc-mode' and buffer naming, mainly
    ;; focusing on adding project context for the current buffer.
    (setq-default mode-line-format
     '("%e" mode-line-front-space
       (:propertize
        ("" mode-line-mule-info mode-line-client mode-line-modified
         mode-line-remote mode-line-window-dedicated)
        display (min-width (6.0)))
       mode-line-frame-identification
       (:eval (list
    	   ;; (or (my/mode-line-project-name)) ""
    	   (gleemacs-modeline-major-mode-indicator) " "
    	   mode-line-buffer-identification ""
    	   ;; (gleemacs/mode-line-path) ""
    	   ))
       " "
       mode-line-position
       (:eval
        (list
         (or (gleemacs/mode-line-project-name))
         (or (gleemacs/mode-line-vc-branch))
         (format-mode-line mode-line-modes)
         (string-trim(format-mode-line mode-line-misc-info))))))


<a id="h:dc83b0a8-dd7a-4a97-a64f-2d14b0362283"></a>

### `uniquify`

    ;; ; `uniquify' (unique names for buffers)
    (use-package uniquify
      :ensure nil
      :custom
      (uniquify-separator " | ")
      :config
      (setq uniquify-buffer-name-style 'forward)
      (setq uniquify-strip-common-suffix t)
      (setq uniquify-after-kill-buffer-p t))


<a id="h:c21457dd-4585-4644-b7d6-73dcd792095d"></a>

### `ace-window`

    ;; ; Window Setup -----------------
    ;; ; Ace Window
    ;; Makes multi window movements efficent and predictable
    (use-package ace-window
      :init
      (global-set-key [remap other-window] #'ace-window)
      :config
      (setq aw-keys '(?a ?s ?d ?f ?g ?h ?j ?k ?l))
      aw-scope 'frame
      aw-background t)


<a id="h:008c887c-1e4b-47bd-8e12-10964e8e29c9"></a>

### `winner`

    ;; ; Window history (winner-mode)
    (use-package winner
      :ensure nil
      :hook (after-init . winner-mode)
      :bind
      (("C-x <right>" . winner-redo)
       ("C-x <left>" . winner-undo)))


<a id="h:017eae8e-db26-434e-b787-c622884ef08b"></a>

### `tab-bar`

    (use-package tab-bar
      :ensure nil
      :config
      (setq tab-bar-new-button-show nil)
      (setq tab-bar-close-button-show nil)
      (setq tab-bar-show 1))


<a id="h:9dae1c55-0ba0-4980-863d-b7f71a0cc91f"></a>

### Footer

    ;; ; Now providing glee...
    (provide 'gleemacs-window)
    
    ;;; gleemacs-window.el ends here


<a id="h:8fef9093-687f-44c8-9208-b18b9a733dbd"></a>

# Cheers and Inspiration

-   **Protesilaos&rsquo; (aka Prot) .dotmacs:** Source: <https://protesilaos.com/emacs/dotemacs>
    
    Prot&rsquo;s config is the gold standard for learning and configuring GNU Emacs.
    It&rsquo;s both a tutorial and an expertly written configuration, and is used
    heavily in *gleemacs*. If you need someone who knows a package inside and out
    from a useability standpoint, it&rsquo;s probably him!

-   **James Cherti&rsquo;s minimal.emacs.d:** Source: <https://github.com/jamescherti/minimal-emacs.d>
    
    James&rsquo; config served as the base line for performance standards in *gleemacs*.
    His setup is buttery smooth and extremely quick to load, and who doesn&rsquo;t like
    that?!

-   **Steve Purcell&rsquo;s emacs.d:** Source: <https://github.com/purcell/emacs.d>
    
    Purcell&rsquo;s config directly inspired the modular layout of *gleemacs*. Initially
    when I read through Prot&rsquo;s config, it seemed extremely complex, Purcell&rsquo;s on
    the other hand (despite being effectively the same as Prot&rsquo;s&#x2026;) just clicked;
    after that, so did Prot&rsquo;s. His `ibuffer` setup was lovingly borrowed as well.

