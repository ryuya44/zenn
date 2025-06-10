---
title: "Windows 365 Frontline 共有モードを展開する方法 -"
emoji: "🚁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Windows", "Microsoft365", "Windows365"]
published: true
---

:::message alert
本記事は、2025 年 06 月の時点での情報となります。
:::

## 1. 概要 - Windows 365 Frontline の共有モードとは- 

![](https://storage.googleapis.com/zenn-user-upload/5c888c80075f-20241204.png)

まず、Windows 365 Frontline は、上記スライドの左側にあたる専用モードと呼ばれる 1 ライセンスで 3 台のクラウド PC が利用できる専用モードがありました。

今回の 4 月に一般提供された共有モードは、1 つのライセンスで、大人数が利用できる共有 PC のようなモードが新しく発表されました。

※ただし、いずれのモードも、アクティブ セッション数はライセンス 1 つにつき 1 までという制限があります。

公開情報 : [Windows 365 Frontline とは | MSLearn ](https://learn.microsoft.com/ja-jp/windows-365/enterprise/introduction-windows-365-frontline#windows-365-frontline-in-shared-mode-preview)
細かい動作などを確認されたい方はクイック スタート ガイドもおすすめです。
[Windows 365 Frontline Cloud PC in shared mode – Quick Start Guide | Microsoft Community Hub](https://techcommunity.microsoft.com/discussions/windows365discussions/windows-365-frontline-cloud-pc-in-shared-mode-%E2%80%93-quick-start-guide/4399905)

## 2. Windows 365 Frontline の共有モードを展開してみる！

大まかな流れとして、3 つのステップがあります。
1. 前提ライセンス (**Entra ID P1, Intune Plan 1, Windows E3**) の付与  
2. Intune 管理センターで利用対象となるユーザーのグループの作成
3. Intune 管理センターでプロビジョニング ポリシーを作成
※ Windows 365 Frontline のライセンスは、プロビジョニング ポリシーの作成時に**グループ**に対して割り当てます。(Windows 365 Enterprise とは異なることに注意！)


:::message
ここからの作業は、前提ライセンスを利用ユーザーに割り当て済みかつ、Windows 365 Frontline のライセンスを保有している(割り当てはしなくて OK )ことから始めます。上記のステップ 2 以降から行います。
購入や試用版ライセンスの入手については以下のサイトをご確認ください。
https://www.microsoft.com/ja-jp/windows-365/enterprise/compare-plans-pricing

ユーザーの作成、ライセンスの付与などの詳細な手順は、以下の記事が参考になると思います。
https://zenn.dev/takuyaot/books/7b576df97e9f22/viewer/39401e
:::




### 2.1 Intune 管理センターでグループを作成する！

1. [Intune 管理センター](https://intune.microsoft.com/) にアクセスします。

2. 左のブレードの [グループ] -> [新しいグループ] の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/155c8fbec8f6-20250603.png)

3. [新しいグループ] をクリックします。以下の内容を設定します。
- グループの種類: セキュリティ
- グループの名前 : お好きな名前
- メンバー : Windows 365 Frontline を利用するユーザー, グループを選択します。
- [保存] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/44a9a14e1eda-20250603.png)

これでグループの作成は完了です。

### 2.2 Intune 管理センターでプロビジョニング ポリシーを作成する！

1. 左のブレードの [デバイス] -> [Windows 365] -> [プロビジョニング ポリシー] -> [ポリシーの作成] の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/8a8607d92dc8-20250602.png)

2. 以下の内容で設定を行い、[次へ] をクリックします。
- 名前 : お好きな名前を入力
- ライセンスの種類 : **Frontline**
- フロントラインの種類 : **共有**
- 結合の種類 : Microsoft Entra に参加
- ネットワーク : Microsoft がホストしているネットワーク
- 地理 : 日本
- リージョン : 東日本
- Microsoft Entra シングル サインオン にチェック
![](https://storage.googleapis.com/zenn-user-upload/1eca0c371bd3-20250602.png)

3. ギャラリー イメージを選択します。今回は既定のまま進みます。
![](https://storage.googleapis.com/zenn-user-upload/c2626df8b7f1-20250603.png)

4. 言語を選択し、[次へ] をクリックします。
※その下に、Windows Autopilot の項目がありますが、共有モードの展開直後から、アプリケーションなどを利用したい場合、プレビュー中の機能ではありますが、Autopilot デバイス準備で展開することも可能です。
公開情報 :[クラウド PC で Autopilot デバイスの準備を使用する | Microsoft Learn](https://learn.microsoft.com/ja-jp/windows-365/enterprise/autopilot-device-preparation)

![](https://storage.googleapis.com/zenn-user-upload/ae552814372a-20250603.png)

5. スコープ タグは、既定のまま [次へ] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/89a7af2b4dca-20250603.png)

6. この画面では、ポリシーの割り当て対象のグループを選択し、何台のクラウド PC をそのグループに割り当てるかを設定します。（※ライセンスの割り当てがここで行われます）
- [グループを追加] をクリックし、割り当て対象のグループを選択し、[選択] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0ba4dcccd14c-20250603.png)

- クラウド PC のサイズをクリックします。
  - 利用可能なクラウド PC を選択します。
  - 割り当て名は、クラウド PC の利用ユーザーに表示される PC 名です。
  - [選択] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/3312716c4774-20250603.png)

7. 構成内容を確認し、[保存] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/a7e453bb30cb-20250603.png)

これでプロビジョニング ポリシーの作成は完了です。

## 3. Windows 365 Frontline の共有モードを使ってみる！

割り当て対象のユーザーに対して、先程のプロビジョニングポリシーで割り当て名に記載した名前で表示されます。
[接続] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0cea3c8ae2c6-20250603.png)

このように、共有モードで展開したクラウド PC にアクセスすることができました！
![](https://storage.googleapis.com/zenn-user-upload/fa504b0ce0e0-20250603.png)

## 4. まとめ
今回は、Windows 365 Frontline 共有モードを展開する方法をご紹介しました！
本ブログがみなさまの参考になれば幸いです😉








