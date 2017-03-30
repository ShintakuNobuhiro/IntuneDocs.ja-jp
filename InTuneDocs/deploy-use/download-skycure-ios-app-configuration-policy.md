---
title: "Skycure iOS アプリ構成ポリシーをダウンロードする | Microsoft Docs"
description: "エンドユーザーに展開した Skycure iOS アプリで使用する Skycure iOS アプリ構成ポリシーをダウンロードします。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: d211b876-4d3a-473c-999f-843c0a16cd22
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-classic
translationtype: Human Translation
ms.sourcegitcommit: e76d66768ac58df25313e102b7f60d2bc7bbc59b
ms.openlocfilehash: b05083e6c5c93a8ed68477341a1ac732019fa764
ms.lasthandoff: 03/22/2017


---

# <a name="download-skycure-ios-app-configuration-policy"></a>Skycure iOS アプリ構成ポリシーをダウンロードする

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

##<a name="before-you-begin"></a>始める前に

次の手順を実行するには、Skycure 管理コンソールにログインする必要があります。

> [!TIP] 
> Microsoft Internet Explorer 11 または Edge を利用しているときは、場合によっては、プライベート モードを利用して Skycure 管理コンソールを開く必要があります。

## <a name="to-download-the-ios-app-configuration-policy"></a>iOS アプリ構成ポリシーをダウンロードするには

1.  [Skycure 管理コンソール](https://aad.skycure.com)に進みます。

2.  自分の **Skycure 管理者資格情報**を入力し、**[続行]** をクリックします。

    ![Skycure 管理コンソールのログイン](../media/mtp/skycure-ios-app-1.png)

    > [!IMPORTANT] 
    > Skycure 管理者のユーザー名は電子メール アカウントですが、そのアカウントは Azure Active Directory の有効なアカウントでなければなりません。有効なユーザーではない場合、ログインは失敗します。 Skycure は、シングル サインオン (SSO) を使用して、管理者ユーザー名の認証に Azure Active Directory を使用します。

3.  **[設定]** &gt; **[Device Management Integrations (デバイス管理統合)]** &gt; **[EMM Integration Selection (EMM 統合選択)]** の順に進み、**[Microsoft Intune]** を選択し、選択を保存します。

2.  **[Integration setup files (統合セットアップ ファイル)]** リンクをクリックし、生成された \*.zip ファイルを保存します。 この .zip ファイルには **skycure\_configuration.plist** ファイルが含まれます。このファイルを利用し、Intune クラシック コンソールで iOS アプリ構成ポリシーが作成されます。

![Skycure 統合セットアップ ファイル](../media/mtp/skycure-ios-app-2.png)

## <a name="next-steps"></a>次のステップ

[Skycure アプリ、Microsoft Authenticator アプリ、iOS 構成ポリシーの追加](https://docs.microsoft.com/intune/deploy-use/add-skycure-apps-microsoft-authenticator-and-ios-app-configuration-policy)
