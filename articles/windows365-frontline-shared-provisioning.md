---
title: "Windows 365 Frontline 共有モードを展開する方法 -"
emoji: "🚁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Windows", "Microsoft365", "Windows365"]
published: false
---

:::message alert
本記事は、2025 年 05 月の時点での情報となります。
:::

## 1. 概要 - Windows 365 Frontline の共有モードとは- 

![](https://storage.googleapis.com/zenn-user-upload/5c888c80075f-20241204.png)

まず、Windows 365 Frontline は、上記スライドの左側にあたる専用モードと呼ばれる 1 ライセンスで 3 台のクラウド PC が利用できる専有モードがありました。

今回の 4 月に一般提供された共有モードは、1 つのライセンスで、大人数が利用できる共有 PC のようなモードが新しく発表されました。

※ただし、いずれのモードも、アクティブ セッション数はライセンス 1 つにつき 1 までという制限があります。

公開情報 : [Windows 365 Frontline とは | MSLearn ](https://learn.microsoft.com/ja-jp/windows-365/enterprise/introduction-windows-365-frontline#windows-365-frontline-in-shared-mode-preview)
細かい動作などを確認されたい方はクイック スタート ガイドもおすすめです。
[Windows 365 Frontline Cloud PC in shared mode – Quick Start Guide | Microsoft Community Hub](https://techcommunity.microsoft.com/discussions/windows365discussions/windows-365-frontline-cloud-pc-in-shared-mode-%E2%80%93-quick-start-guide/4399905)

## 2. Windows 365 Frontline の共有モードを展開してみる

大まかな流れとして、3 つのステップがあります。
1. Entra 管理センターで展開するユーザー グループの作成
2. 前提ライセンス (Entra ID P1, Intune Plan 1, Windows E3) の付与 
3. Intune 管理センターでプロビジョニング ポリシーを作成


:::message
ここからの作業は Windows 365 Frontline のライセンスを保有していることから始めます。
購入や試用版ライセンスの入手については以下のサイトをご確認ください。
https://www.microsoft.com/ja-jp/windows-365/enterprise/compare-plans-pricing
:::

ユーザーの作成、ライセンスの付与などの詳細な手順は、以下の記事が参考になると思います。
https://zenn.dev/takuyaot/books/7b576df97e9f22/viewer/39401e

今回、Windows 365 Frontline の利用する**ユーザー**に割り当てる必要があるのは、**Microsoft Entra ID P1, Intune Plan 1, Windows E3** を含むライセンスです。

Windows 365 Frontline のライセンスは、Intune のポータル上で**グループ**に対して割り当てます。

### Entra 管理センターでグループを作成する

[Entra 管理センター](https://entra.microsoft.com/) にアクセスします。

左のブレードの ID > グループ > すべてのグループ をクリックします。
[新しいグループ] をクリックします。
グループ名を入力します。
グループに展開したいユーザーを追加します。
保存をクリックします。

これでグループの作成は完了です。

### Intune 管理センターでプロビジョニング ポリシーを作成する

1. [Intune 管理センター](https://intune.microsoft.com/) にアクセスします。

2. 左のブレードの [デバイス] -> [Windows 365] -> プロビジョニング ポリシーの順にクリックします。
[ポリシーの作成] をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/8a8607d92dc8-20250602.png)

3. 以下の内容で設定を行い次へをクリックします。
- 名前 : お好きな名前を入力
- ライセンスの種類 : **Frontline**
- フロントラインの種類 : **共有**
- 結合の種類 : Microsoft Entra に参加
- ネットワーク : Microsoft がホストしているネットワーク
- 地理 : 日本
- リージョン : 東日本
- Microsoft Entra シングル サインオン 

![](https://storage.googleapis.com/zenn-user-upload/1eca0c371bd3-20250602.png)

イメージを選択します。今回は既定のまま進みます。
![](https://storage.googleapis.com/zenn-user-upload/c2626df8b7f1-20250603.png)

言語を選択します。その下に、Windows Autopilot の項目がありますが、こちらは、公開情報を参考にしてください。
![](https://storage.googleapis.com/zenn-user-upload/ae552814372a-20250603.png)
保存をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/89a7af2b4dca-20250603.png)

![](https://storage.googleapis.com/zenn-user-upload/0ba4dcccd14c-20250603.png)

![](https://storage.googleapis.com/zenn-user-upload/3312716c4774-20250603.png)

![](https://storage.googleapis.com/zenn-user-upload/a7e453bb30cb-20250603.png)
これでプロビジョニング ポリシーの作成は完了です。

## Windows 365 Frontline の共有モードを使ってみる

共有モードの展開直後から、アプリケーションなどを利用したい場合、プレビュー中の機能ではありますが、Autopilot デバイス準備で展開することも可能です。
公開情報 :[クラウド PC で Autopilot デバイスの準備を使用する | Microsoft Learn](https://learn.microsoft.com/ja-jp/windows-365/enterprise/autopilot-device-preparation)

![](https://storage.googleapis.com/zenn-user-upload/68c20a31165f-20250603.png)

![](https://storage.googleapis.com/zenn-user-upload/fa504b0ce0e0-20250603.png)
## 5. まとめ
今回は、Windows 365 Frontline 共有モードを展開する方法をご紹介しました！
本ブログがみなさまの参考になれば幸いです😉








