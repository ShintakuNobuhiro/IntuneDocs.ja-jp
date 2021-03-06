---
title: "Microsoft Intune - Azure でデバイスをリモートで管理する | Microsoft Docs"
description: "TeamViewer を使用するために必要なロールの表示、TeamViewer コネクタのインストール方法、Azure Portal で Microsoft Intune を使用してデバイスをリモートで管理する方法の段階的なガイダンス"
keywords: 
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/01/2018
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 64f6dd6bf787a6f590655f03ac8f04312836e0b5
ms.sourcegitcommit: 7e5c4d43cbd757342cb731bf691ef3891b0792b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2018
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>TeamViewer を使用して、Intune デバイスをリモートで管理する

Intune で管理されているデバイスは、[TeamViewer](https://www.teamviewer.com) を使用してリモートで管理できます。 TeamViewer は、個別に購入するサード パーティ プログラムです。 このトピックでは、Intune 内で TeamViewer を構成して、リモートでデバイスを管理する方法を示します。 

## <a name="prerequisites"></a>必要条件

- サポートされているデバイスを使用します。 Intune で管理された Android デバイスと Windows デバイスでは、リモート管理がサポートされます。 TeamViewer で Windows Holographic (HoloLens)、Windows Team (Surface Hub)、または Windows 10 S がサポートされない場合があります。サポートについては、[TeamViewer](https://www.teamviewer.com) で更新情報を確認してください。

- Azure Portal 内の Intune 管理者には、次の [Intune ロール](role-based-access-control.md)が必要です。  

    - **リモート アシスタンスの更新**: 管理者に TeamViewer コネクタの設定の変更を許可します。
    - **リモート アシスタンスの要求**: 管理者にすべてのユーザーに対して新しいリモート アシスタンス セッションを開始することを許可します。 このロールを持つユーザーは、スコープ内のどの Intune ロールにも制限されません。 また、スコープ内で Intune ロールが割り当てられたユーザーまたはデバイス グループも、リモート アシスタンスを要求することができます。 

- サインイン資格情報を持つ [TeamViewer](https://www.teamviewer.com) アカウント

TeamViewer を使用すると、Intune コネクタ用 TeamViewer での TeamViewer セッションの作成、Active Directory データの読み取り、TeamViewer アカウント アクセス トークンの保存を許可することになります。

## <a name="configure-the-teamviewer-connector"></a>TeamViewer コネクタの構成

デバイスにリモート アシスタンスを提供するには、以下の手順で Intune TeamViewer コネクタを構成します。

1. [Azure Portal](https://portal.azure.com) で、**[すべてのサービス]** を選択し、**Microsoft Intune** を検索します。
2. **Microsoft Intune** で、**[デバイス]**、**[TeamViewer Connector]** の順に選択します。
3. **[接続]** を選択し、使用許諾契約書に同意します。
4. **[TeamViewer にログインして承認する]** を選択します。
5. TeamViewer サイトの Web ページが開きます。 TeamViewer ライセンスの資格情報を入力して、**サインイン**します。

## <a name="remotely-administer-a-device"></a>デバイスをリモートで管理する

コネクタを構成したら、デバイスをリモートで管理する準備ができました。 次の手順を使用します。 

1. [Azure Portal](https://portal.azure.com) で、**[すべてのサービス]** を選択し、**Microsoft Intune** を検索します。
2. **Microsoft Intune** で、**[デバイス]**、**[すべてのデバイス]** の順に選択します。
3. リストから、リモートで管理するデバイスを選択します。 デバイスのプロパティで、**[新しいリモート アシスタンス セッション]** を選択します。
4. Intune を TeamViewer サービスに接続すると、デバイスの情報が表示されます。 **接続**してリモート セッションを開始します。

![TeamViewer を使用して Android デバイスをリモート管理する - 例](./media/android-teamviewer.png)

リモート セッションを開始すると、エンド ユーザーのデバイスのポータル サイト アプリのアイコンに通知フラグが表示されます。 通知は、アプリを開いたときにも表示されます。 その後、ユーザーはリモート アシスタンス要求を受け入れることができます。

TeamViewer では、デバイスの制御など、デバイスでさまざまな操作を完了できます。 実行できる操作の詳細については、[TeamViewer ガイダンス](https://www.teamviewer.com/support/documents/)を参照してください。

完了したら、TeamViewer ウィンドウを閉じます。