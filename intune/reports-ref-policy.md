---
title: "ポリシー | Microsoft Docs"
description: "Intune データ ウェアハウス API のエンティティ コレクションのポリシー カテゴリに関するリファレンス トピック。"
keywords: "Intune データ ウェアハウス"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: D5ADB9D8-D46A-43BD-AB0F-D6927508E3F4
ms.reviewer: jeffgilb
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 6af0ff1f463c153e62f6df63ce811076c5f692f2
ms.sourcegitcommit: addf6a40caa22c22adfd2e2eff7d666cd1877e3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2017
---
# <a name="reference-for-policy-entities"></a>ポリシー エンティティのリファレンス

**ポリシー** カテゴリには、次のような情報を追跡するモバイル デバイスのエンティティが含まれています。

  -  デバイス構成プロファイル、アプリ構成プロファイル、およびコンプライアンス ポリシーのインベントリ  
  -  成功、保留中、失敗、またはエラー状態のデバイス数/日  
  -  成功、保留中、失敗、またはエラー状態のユーザー数/日  
  -  成功、保留中、失敗、またはエラー状態のデバイスの累積数  

## <a name="policy"></a>ポリシー

**Policy** エンティティには、デバイス構成プロファイル、アプリ構成プロファイル、およびコンプライアンス ポリシーが表示されます。 モバイル デバイス管理 (MDM) を含むポリシーを社内のグループに割り当てることができます。

| プロパティ  | 説明 | 例 |
|---------|------------|--------|
| PolicyKey |データ ウェアハウス内のポリシーを表す一意のキー |123 |
| PolicyId |データ ウェアハウス内のポリシーを示す一意識別子 |b66bc706-ffff-7437-0340-032819502773 |
| PolicyName |ポリシーの名前 |"Windows 10 Baseline" |
| PolicyVersion |ポリシーのバージョン。 ポリシーを編集または変更すると、新しいバージョンが作成されます。 |1, 2, 3 |
| IsDeleted |ポリシー レコードが更新されているかどうかを示します。  True - ポリシーには、フィールドが更新された新しいレコードがあります。 False - ポリシーの最新のレコードです。 |真/偽 |
| StartDateInclusiveUTC |ポリシーがデータ ウェアハウスで作成されたときの UTC 日時 |11/23/2016 12:00:00 AM |
| DeletedDateUTC |IsDeleted が True に変更されたときの UTC 日時 |11/23/2016 12:00:00 AM |
| RowLastModifiedDateTimeUTC |ポリシーがデータ ウェアハウスで最後に変更されたときの UTC 日時 |11/23/2016 12:00:00 AM |

## <a name="policytype"></a>PolicyType

**PolicyType** エンティティには、デバイス構成プロファイル、アプリ構成プロファイル、およびコンプライアンス ポリシーの種類が表示されます。 モバイル デバイス管理 (MDM) を含むポリシーを社内のグループに割り当てることができます。

| プロパティ  | 説明 | 例 |
|---------|------------|--------|
| PolicyTypeId |ソース システムのポリシーを示す一意識別子 |123 |
| PolicyTypeKey |データ ウェアハウス内のポリシーを示す一意識別子 |1 |
| PolicyTypeName |ポリシーの種類の名前 |Windows 10 のコンプライアンス ポリシー |

## <a name="deviceconfiguration"></a>DeviceConfiguration

**DeviceConfigurationProfileDeviceActivity** エンティティには、成功、保留中、失敗、エラー状態のデバイス数/日が表示されます。 この数は、エンティティに割り当てられているデバイス構成プロファイルを反映しています。 たとえば、割り当てられているすべてのポリシーでデバイスが成功状態の場合、その日の成功カウンターが 1 つ増えます。 成功状態のプロファイルとエラー状態のプロファイルという 2 つのプロファイルがデバイスに割り当てられている場合、エンティティは成功カウンターを増やし、デバイスをエラー状態にします。 エンティティには、過去 30 日間の各状態のデバイス数/日が表示されます。

| プロパティ  | 説明 | 例 |
|---------|------------|--------|
| DateKey |デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー |20160703 |
| Pending |保留状態の一意のデバイス数 |123 |
| 成功 |成功状態の一意のデバイス数 |12 |
| エラー |エラー状態の一意のデバイス数 |10 |
| Failed |失敗状態の一意のデバイス数 |2 |

## <a name="userconfiguration"></a>UserConfiguration

**UserConfigurationProfileDeviceActivity** エンティティには、成功、保留中、失敗、エラー状態のユーザー数/日が表示されます。 この数は、エンティティに割り当てられているデバイス構成プロファイルを反映しています。 たとえば、割り当てられているすべてのポリシーでユーザーが成功状態の場合、その日の成功カウンターが 1 つ増えます。 成功状態のプロファイルとエラー状態のプロファイルという 2 つのプロファイルがユーザーにある場合、そのユーザーはエラー状態とカウントします。  **UserConfigurationProfileDeviceActivity** エンティティには、過去 30 日間の各状態のユーザー数/日が表示されます。

| プロパティ  | 説明 | 例 |
|---------|------------|--------|
| DateKey |デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー |20160703 |
| Pending |保留状態の一意のユーザー数 |123 |
| 成功 |成功状態の一意のユーザー数 |12 |
| エラー |エラー状態の一意のユーザー数 |10 |
| Failed |失敗状態の一意のユーザー数 |2 |

## <a name="policytypeactivity"></a>PolicyTypeActivity

**PolicyTypeActivity** エンティティには、成功、保留中、失敗、またはエラー状態のデバイスの累積数が表示されます。 デバイス構成プロファイル、アプリ構成プロファイル、またはコンプライアンス ポリシーについて、これらの状態が 1 日単位で表示されます。

| プロパティ  | 説明 | 例 |
|---------|------------|--------|
| DateKey |デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー |20160703 |
| PolicyKey |ポリシー キーとポリシーを結合して、policyName を取得できます |Windows 10 baseline |
| PolicyTypeKey |ポリシー キーの種類とポリシーの種類を結合してポリシーの種類名を取得できます |Windows10Compliance Policy |
| Pending |保留状態の一意のデバイス数 |123 |
| 成功 |成功状態の一意のデバイス数 |12 |
| エラー |エラー状態の一意のデバイス数 |10 |
| Fail- |失敗状態の一意のデバイス数 |2 |