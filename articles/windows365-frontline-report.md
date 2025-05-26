---
title: "Windows 365 - Intune から確認できるレポート, 監視機能について -"
emoji: "🚁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Windows", "Microsoft365", "Windows365","Tech" ]
published: false
---

:::message alert
本記事は、2025 年 05 月の時点での情報となります。
:::

## 1. 概要
Intune 管理センターでは、Windows 365 に特化したレポート機能があること知っていますか？
今回は、Windows 365 のレポート機能について紹介できればと思います。

:::message
ポイント 
:::

### この機能のメリット
管理者は、エンドユーザーが利用している Windows 365 の使用状況などの情報は、スペックやデバイス数を最適化する一助になると考えられます。
また、一部の Windows 365 frontline で展開してるデバイスについて、最大接続数を確認することができます。

#### 公開情報：[クラウド PC を移動する | Microsoft Learn ](https://learn.microsoft.com/ja-jp/windows-365/enterprise/move-cloud-pc)
[クラウド PC アクション](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pc-actions)
[クラウド PC 接続品質レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pc-connection-quality)
[クラウド PC の推奨事項](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[クラウド PC 使用率レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[利用できないクラウド PC](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[接続されている Frontline クラウド PC レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-connected-frontline-cloud-pcs)
[リソース パフォーマンス レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-resource-performance)
[クラウド PC のリージョン間ディザスター リカバリー状態レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/cross-region-disaster-recovery-report)

## 2.試してみる！ 

### 2.1 構成の説明
1. クラウド PC を日本の東リージョンに展開しています。ネットワークは Microsoft Hosted Network を利用しています。
※リージョンは自動を選択することが推奨されています。今回は検証のため東日本にしました。
![](https://storage.googleapis.com/zenn-user-upload/c674c31754d6-20250520.png)
このポリシーで展開されたクラウドPC CPC-ryuya-67E4K を今回移動させる対象とします。
![](https://storage.googleapis.com/zenn-user-upload/a0dbb159b327-20250520.png)




### 2.2 クラウド PC を移動してみる！

1. 移動させるクラウド PC を展開したポリシーを選択します。
![](https://storage.googleapis.com/zenn-user-upload/b6bcfa264212-20250520.png)

2. 当該ポリシーをクリックすると、構成内容が表示されます。全般の右隣の "編集" をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0d81ba995a1e-20250520.png)


3. 移動先のリージョンあるいはネットワークを選択し、"次へ" をクリックします。今回は、地理をドイツにします。
※今回はリージョンの移動にしましたが、ネットワークの移動でも可能です。
![](https://storage.googleapis.com/zenn-user-upload/7ffae5d40d92-20250520.png)


4. 構成内容を確認の上、"更新" をクリックします
![](https://storage.googleapis.com/zenn-user-upload/5be94379ccf0-20250520.png)


5. "この構成を適用" をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/2c9f828d8173-20250520.png)

6. 今回は一台のみ、別リージョンに移動したいので、"選択したデバイスにリージョンまたは Azure ネットワーク接続" を選択し、"適用" をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/8d88e22bbe47-20250520.png)


7. デバイスの選択画面が表示されます。このプロビジョニングポリシーで展開している クラウド PC から移動するデバイスを選択し、画面下部の "選択" をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/151146583cb9-20250520.png)
これで、選択したデバイスに対して、別リージョンに移動する手順は完了です！


## 3. 移動中のクラウド PC の状態を監視してみる！
1. Microsoft Intune 管理センター の左のブレードの デバイス > 監視 > クラウド PC アクション（プレビュー）の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/8aee55451c73-20250520.png)


2. クラウド PC の過去 90 日間のアクションの状態を表示されます。移動の対象デバイスについて、アクションがリージョンの移動、状態が "進行中" と確認できます。
![](https://storage.googleapis.com/zenn-user-upload/945b10640b0f-20250520.png)
完了すると状態が、"成功" になります。
![](https://storage.googleapis.com/zenn-user-upload/ef4853d4ec90-20250520.png)


## 4. ラウンドトリップを計測してみる!

- 移動前
接続元 : 東京
接続先のクラウド PC : 日本
ラウンドトリップ : 8 ミリ秒
![](https://storage.googleapis.com/zenn-user-upload/ade62bbc2088-20250520.png)

- 移動後
接続元 : 東京
接続先のクラウド PC : ドイツ
ラウンドトリップ : 280 ミリ秒
![](https://storage.googleapis.com/zenn-user-upload/8ebd35208a64-20250520.png)
移動後、ラウンドトリップが大きくなったので、無事に移動できたことが確認できました！


## 5. まとめ
今回は展開済みのクラウド PC を移動する方法をご紹介しました！
本ブログがみなさまの参考になれば幸いです😉








