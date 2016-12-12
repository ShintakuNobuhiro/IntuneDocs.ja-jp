---
title: "アプリと MAM CA の使用 | Microsoft Intune"
description: "MAM CA を利用して、O365 サービスに対してアクセス権を持つアプリを制御する方法の概念について説明します。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 10/24/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 71dcf9bc-bfd1-4e06-b7ad-14b33a2288d0
ms.reviewer: chrisgre
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 87e37cd8334ddb9331c0662b691545cd0ab0553a
ms.openlocfilehash: 317d101c34854fdf4913adcf53bdef614599deb7


---
# <a name="what-to-expect-when-using-an-app-with-mam-ca"></a>アプリと MAM CA を使用する場合の結果
MAM CA は、デバイス上に必ずあるブローカー アプリを利用して、承認されたアプリケーションの ID を確認します。
*  **iOS** の場合、**Azure Authenticator アプリ**がブローカー アプリです。
* **Android** の場合、**Intune ポータル サイト アプリ**がブローカー アプリです。 

OneDrive や Outlook など、MAM CA でサポートされているアプリにエンドユーザーが初めてサインインする場合、ブローカー アプリをインストールし、デバイスを Azure AD に登録するように求められます。 Azure AD にデバイスを登録すると (以前は社内参加と呼ばれていました)、トークンの発行先に対してデバイス レコードと証明書が作成されます。  これは **MDM の登録**と**同じではありません**。 適用される管理プロファイルまたはポリシーはありません。また、デバイスのアプリから取得されるインベントリはありません。  ブローカー アプリのインストールとデバイスの登録プロセスは、管理対象アプリを初めて使用する場合にのみ実行されます。

次の一覧は、デバイスから直接派生するプロパティです。

* alternativeSecurityIds (Azure Active Directory 証明書の拇印と公開キー ハッシュ)
* deviceOSType
* deviceOSVersion
* displayName

## <a name="to-remove-a-device-from-azure-ad-registration"></a>Azure AD の登録からデバイスを削除するには
デバイスの登録は、Azure AD 管理コンソールで削除することができます。通常、IT 管理者が削除を実行します。  また、エンドユーザーが自分のデバイスで削除することもできます。

* **Azure AD 管理コンソール**: Azure AD 管理コンソール**で、対象のデバイスを削除します。
* **iOS デバイス**: Azure Authenticator アプリを開き、アカウントを左にスワイプし、登録の解除を選択します。  
* **Android デバイス**: ポータル サイト アプリをアンインストールするか、**[システム設定]** からアカウントを削除します。



## <a name="mam-ca-with-conditional-access-based-on-device-compliance"></a>MAM CA とデバイスのコンプライアンスに基づく条件付きアクセス  

[Intune 管理コンソール](https://manage.microsoft.com)または [Azure AD Premium 管理コンソール] (https://manage.windowsazure.com) で[デバイスのコンプライアンスに基づいて条件付きアクセス](restrict-access-to-email-and-o365-services-with-microsoft-intune.md) (**デバイス CA**) を構成できます。 デバイス CA を使用する場合、ユーザーが Exchange Online に接続するには、Intune デバイス コンプライアンス ポリシーに準拠している Intune の管理対象デバイス、またはドメインに参加しているコンピューターを使用する必要があります。  ユーザーが、MAM CA とデバイス CA ポリシー両方の対象である 1 つまたは複数のセキュリティ グループに属している場合、ユーザーは次の 2 つの要件のうち 1 つを満たす必要があります。
* サービスへのアクセスに使用されるアプリは、MAM CA でサポートされているモバイル アプリであり、アプリを実行するデバイスには、**iOS Authenticator (iOS デバイスの場合)** または**ポータル サイト アプリ (Android デバイスの場合)** がインストールされている。
* サービスへのアクセスに使用されるデバイスは、**Intune の管理対象で Intune のデバイス コンプライアンス ポリシーに準拠している**か、**ドメインに参加しているコンピューター**である。  わかりやすい例を示します。
  * ユーザーが**ネイティブ iOS 電子メール アプリ**から接続する場合、ネイティブ電子メール アプリは MAM CA でサポートされていないため、**管理対象で準拠しているデバイス**を使用して接続する必要があります。
  * ユーザーが **Windows Home コンピューター**から接続する場合、**デバイス CA ポリシー**が適用されるので、ドメインに参加しているコンピューターを使用する必要があります。




## <a name="next-steps"></a>次のステップ
[MAM アプリ用の Exchange Online ポリシーを作成する](mam-ca-for-exchange-online.md)

[最新の認証を使用していないアプリをブロックする](block-apps-with-no-modern-authentication.md)

### <a name="see-also"></a>関連項目

[MAM ポリシーでアプリ データを保護する](protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)



<!--HONumber=Dec16_HO2-->

