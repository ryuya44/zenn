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

## はじめに
ここでは 2024 年 11 月の Microsoft の技術カンファレンスである Ignite で発表された Windows 365 frontline の共有モードの展開・利用をした内容を紹介します。
公式ドキュメントは[こちら](https://learn.microsoft.com/ja-jp/windows-365/enterprise/introduction-windows-365-frontline#windows-365-frontline-in-shared-mode-preview)
:::message alert
本機能は、プレビュー中のものであり、GA（一般公開）時とは異なる動作になる可能性がございます。
:::

## 目次

- はじめに
- Windows 365 Frontline の共有モードとは
    - 共有モードの概要
    - ＜共有モードの利用シナリオ＞営業ぽくなるからいらないかな
- 共有モードを展開する
- 共有モードを使ってみる
    - サインインエクスペリエンス
    - 先に使っている人がいる状態で使ってみるとどうなる
- まとめ

## Windows 365 Frontline の共有モードとは
![](https://storage.googleapis.com/zenn-user-upload/5c888c80075f-20241204.png)

前提として、Windows 365 Frontline は、上記スライドの左側にあたる専用モードと呼ばれる 1 ライセンスで 3 台のクラウド PC が利用できるモードがありました。

今回の Ignite で、上記スライドの右側にあたる共有モードは、1 つのライセンスで、大人数が利用できる共有 PC のようなモードが新しく発表されました。

※ただし、いずれのモードも、アクティブ セッション数はライセンス 1 つにつき 1 までという制限があります。

[公式ドキュメント](https://learn.microsoft.com/ja-jp/windows-365/enterprise/introduction-windows-365-frontline#windows-365-frontline-in-shared-mode-preview)に注意がありました。一般公開時に、確認する必要がありそうですね。
以下公式ドキュメントを抜粋

:::message alert

注意
パブリック プレビュー中に、共有クラウド PC に割り当てられたユーザーの潜在的な制限を評価しています。 詳細については、一般公開時に共有されます。

:::

## Windows 365 Frontline の共有モードを展開してみる

大まかな流れとして、2 つのステップがあります。
- Entra 管理センターで展開するユーザー グループを作成
- Intune 管理センターでプロビジョニング ポリシーを作成する

また今回はネットワークをホストネットワークを選択し、展開します。

:::message
ここからの作業は Windows 365 frontline のライセンスを保有していることから始めます。
購入や試用版ライセンスの入手については以下のサイトをご確認ください。
https://www.microsoft.com/ja-jp/windows-365/enterprise/compare-plans-pricing
:::

ユーザーの作成、ライセンスの付与などの詳細な手順は、以下の記事を参考にしてください。
https://zenn.dev/takuyaot/books/7b576df97e9f22/viewer/39401e

今回、**ユーザー**に割り当てる必要があるのは、「Microsoft Entra ID P1」「Intune」「Windows E3」などの前提条件を含むライセンスです。
もちろん展開するグループに対して、ライセンスを割りあてていただいてもかまいせん。

Windows 365 frontline のライセンスは、Intune のポータル上で**グループ**に対して割り当てます。

### Entra 管理センターでグループを作成する

[Entra 管理センター](https://entra.microsoft.com/) にアクセスします。

左のブレードの ID > グループ > すべてのグループ をクリックします。
[新しいグループ] をクリックします。
グループ名を入力します。
グループに展開したいユーザーを追加します。
保存をクリックします。

これでグループの作成は完了です。

### Intune 管理センターでプロビジョニング ポリシーを作成する

[Intune 管理センター](https://intune.microsoft.com/) にアクセスします。

左のブレードのデバイス をクリックします。
左から二つ目のブレードの Windows 365 をクリックします。
プロビジョニング ポリシーをクリックします。
[ポリシーの作成] をクリックします。

ポリシー名を入力します。


保存をクリックします。

これでプロビジョニング ポリシーの作成は完了です。

## Windows 365 Frontline の共有モードを使ってみる


## 5. まとめ
今回は展開済みのクラウド PC を移動する方法をご紹介しました！
本ブログがみなさまの参考になれば幸いです😉








