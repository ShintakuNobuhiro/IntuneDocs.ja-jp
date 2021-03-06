---
title: ロールアウト コミュニケーション計画の作成
titlesuffix: Microsoft Intune
description: この記事は、Microsoft Intune を展開するためのロールアウト コミュニケーション計画を作成する場合に役立ちます。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 10/30/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 393ebe75-d001-485a-b81c-6361c8b5e6ee
ms.reviewer: jeffbu, cgerth
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: b985b92b4ea68fedba3c0d04e53c1e6116a64015
ms.sourcegitcommit: e30fb2375fb79f67e5c1e4ed7b2c21fb9ca80c59
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/17/2018
---
# <a name="develop-a-rollout-communication-plan"></a>ロールアウト コミュニケーション計画の作成

適切な変更管理が行えるかどうかは、今後の変更に関する明確で有益な情報伝達にかかっています。 Intune の展開を円滑に進めるには、ロールアウト コミュニケーション計画に次の 4 つの領域を含める必要があります。

-   伝達する情報

-   伝達に使用する配信方法

-   情報を受け取るユーザー

-   情報伝達のタイムライン

それぞれの領域について詳しく説明します。

## <a name="what-needs-to-be-communicated"></a>伝達する必要がある情報

伝達する情報は、Intune ロールアウト プロセスのどの段階で伝達するかによって異なります。 組織によっては、Intune ロールアウトのキックオフ、登録前、登録後の順に、組織グループとユーザーに段階的に伝達する場合があります。 各段階で伝達される可能性がある情報の種類について説明します。

**キックオフ段階** <br/>Intune プロジェクト自体を紹介する広範な情報伝達。 Intune の概要や Intune を採用する理由 (組織やユーザーにとっての利点) などの質問に答え、展開とロールアウトに関する計画の概要を説明します。

**登録前段階**<br/> Intune と補助的なサービス (Office、Outlook、OneDrive など) に関する情報、組織グループとユーザーが Intune を受け取る予定に関するユーザー リソースと具体的なタイムラインを含む広範な情報伝達。

**登録段階**<br/> Intune を受け取る予定の組織グループ/ユーザーを対象にした情報伝達。 Intune を受け取る準備が整ったことをユーザーに知らせ、登録手順と、サポートや質問の窓口に関する情報を伝えます。

**登録後段階**<br/> Intune に登録された組織グループ/ユーザーを対象とする情報伝達。 ユーザーに役立つ追加のリソースを提供し、登録時と登録後の使用感に関するフィードバックを収集します。

こちらの [エンドユーザー登録ガイド](https://gallery.technet.microsoft.com/Intune-End-User-Enrollment-3a0c9b0c?WT.mc_id=Blog_Intune_General_PCIT) もお役立てください。 そのまま使用することも、組織に合わせて変更することもできます。

## <a name="communication-delivery-methods"></a>情報の配信方法

Intune ロールアウトに関する情報を対象となる組織グループとユーザーに伝達するには、いくつかの配信方法があります。 次の一覧では、情報の配信方法の例とその方法を使用する段階を示しています。

-   組織全体を対象にした対面の会議または Skype 会議 (キックオフ段階)

-   電子メール (登録前段階、登録段階、登録後段階)

-   組織の Web サイト (すべての段階)

-   Yammer、ポスター、チラシ (キックオフ段階、登録前段階)

## <a name="communications-timeline"></a>情報伝達のタイムライン

伝達する必要がある内容と使用する情報伝達方法を決めたら、次の手順は、情報を伝達するタイミングと相手など、情報伝達のタイムラインを決めることです。

たとえば、最初の Intune プロジェクト キックオフの情報伝達は、組織全体または一部のみを対象にして、Intune ロールアウトを開始する数週間前に行います。 次に、Intune ロールアウト スケジュールに合わせて組織グループとユーザーに段階的に伝えます。 次の例は、Intune ロールアウトの情報伝達の大まかな計画のサンプルです。

  | **情報伝達計画** | **7 月** | **8 月** | **9 月** | **10 月** |
|:---:|:---:|:---:|:---:|:---:|
| 段階 1  | すべて |  |  |  |                                                         
| キックオフ会議 | 第 1 週 |  |  |  |                                                         
| 段階 2 | IT 部門 | 営業/マーケティング | 小売 | 人事、財務、幹部 |
| ロールアウト前電子メール 1 | 第 1 週 | 第 1 週 | 第 1 週 | 第 1 週 |
| 段階 3 | IT 部門 | 営業/マーケティング | 小売 | 人事、財務、幹部 |
| ロールアウト前電子メール 2 | 第 2 週 | 第 2 週 | 第 2 週 | 第 2 週 |
| 段階 4 | IT 部門 | 営業/マーケティング | 小売 | 人事、財務、幹部 |
| 登録電子メール | 第 3 週 | 第 3 週 | 第 3 週 | 第 3 週 |
| 段階 5 | IT 部門 | 営業/マーケティング | 小売 | 人事、財務、幹部 |
| 登録後電子メール | 第 4 週 | 第 4 週 | 第 4 週 | 第 4 週 |

[上記の表のテンプレートをダウンロード](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) してコミュニケーション計画を作成することができます。

## <a name="next-step"></a>次の手順

次のセクションは、[サポート計画](planning-guide-support-plan.md)を立てる場合のガイダンスです。
