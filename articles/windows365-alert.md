---
title: "Windows 365 - クラウド PC 用の Intune のアラート機能を試す -"
emoji: "🚁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Windows", "Microsoft365", "Windows365","Tech" ]
published: false
---

:::message alert
本記事は、2025 年 09 月の時点での情報となります。
:::

## 1. 概要
Intune の管理センターに、クラウド PC 用のアラート機能があること知っていますか？
今回は、その機能を紹介しつつ、試してみたいと思います。
ちなみにアラート機能は以下のようにたくさんあります！

![](https://storage.googleapis.com/zenn-user-upload/9a205cb54922-20250901.png)


### この機能のメリット
1. 問題をすぐに発見できる
クラウド PC で「接続できない」「プロビジョニングに失敗した」「イメージのアップロードにエラーが出た」などのトラブルが起きたときに、すぐに通知が届きます。
→ 早く気づけるので、すぐに対応できます。
2. 同時利用のしきい値もチェックできる
Windows 365 Frontline では、同時に使えるクラウド PC の数に制限があります。
その上限に近づいたり、超えたりしたときにも通知が来るので、使いすぎによるトラブルを防げます。
3. 通知方法が選べる
通知は、Microsoft Intune 管理センターにポップアップで表示されます。
さらに、メール通知を有効にすることも可能なので、外出中でも気づけます。
4. アラートの内容をカスタマイズできる
最初から用意されているアラートルール（組み込みルール）を、自分の環境に合わせて変更できます。
→ 必要な情報だけを受け取れるように調整できます。

#### 公開情報：[Windows 365のアラート | Microsoft Learn ](https://learn.microsoft.com/ja-jp/windows-365/enterprise/alerts)
[クラウド PC アクション](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pc-actions)
[クラウド PC 接続品質レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pc-connection-quality)
[クラウド PC の推奨事項](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[クラウド PC 使用率レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[利用できないクラウド PC](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-cloud-pcs-not-available)
[接続されている Frontline クラウド PC レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-connected-frontline-cloud-pcs)
[リソース パフォーマンス レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/report-resource-performance)
[クラウド PC のリージョン間ディザスター リカバリー状態レポート](https://learn.microsoft.com/ja-jp/windows-365/enterprise/cross-region-disaster-recovery-report)

## 2.試してみる！ 
今回は、アラート機能の一つである、"Frontline クラウド PC がコンカレンシー制限に近づいています (プレビュー)" を試してみます。

:::message
ポイント Windows 365 Frontline の最大接続数をこの機能で監視することができます。
:::

### 2.1 アラート ルールの設定
まずは、アラート ルールを作成してみます。





### 2.2 

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








