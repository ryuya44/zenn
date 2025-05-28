---
title: "Entra ID - QR コード認証を試してみる！ -"
emoji: "🚁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Windows", "Microsoft365", "Windows365","Tech" ]
published: false
---

:::message alert
本記事は、2025 年 05 月の時点での情報となります。
:::

## 1. 概要
Entra ID の認証方法として、QR コード認証がプレビューされました！
現時点では、iOS と Android に対応しています。
フロントラインワーカーの抱える課題として、サインインする際に、ユーザー名とパスワードを入力する手間があります。
以下の公開情報にも記載のように、フロントラインワーカーに対して、ＱＲコード認証はシンプルな認証方法を提供します。以下の公開情報に記載のとおり、QR コード認証と条件付きアクセス ポリシーを併用し、セキュアにすることを推奨されています。


公開情報：[ Simplify frontline workers’ sign-in experience with QR code authentication ](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/simplify-frontline-workers%E2%80%99-sign-in-experience-with-qr-code-authentication/3822034)


:::message
ポイント QR コード認証は、QR コードスキャンと PIN の入力のみでサインインするが可能です。
:::


## 2.試してみる！

### 2.1 構成の説明
1. 今回は Entra ID の共有デバイス モードの Android デバイスで、QR コード認証を試してみます。


### 2.2 QR コード認証方法を有効化する！


以下の公開情報に沿って検証してみます。細かい前提条件を確認されたい場合、以下の公開情報が参考になります。
#### 公開情報：[ Microsoft Entra ID の認証方法 - QR コード認証方法 (プレビュー) ](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/simplify-frontline-workers%E2%80%99-sign-in-experience-with-qr-code-authentication/3822034)

1. 少なくとも認証ポリシー管理者以上で Entra 管理センター (https://entra.microsoft.com)にアクセスします。
左のブレードの [保護]->[認証方法]-> QR コード認証(プレビュー) の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0440a92022f3-20250526.png)


2. QR コード認証の設定画面が表示されます。この表示画面では、ＱＲコード認証の有効化と有効化するグループ選択します。
今回は、FLW というグループを選択しました。次に構成をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/2257562b6e5a-20250526.png)


3. この画面では、QR コード認証で利用する PIN の長さ(8 桁以上 20 桁以下です。)と QR コードの有効期限 ( 1 日以上 395 日以下) の設定ができます。今回は既定 (365 日) のまま進みます。
![](https://storage.googleapis.com/zenn-user-upload/9dfea5e545a7-20250526.png)


4. QR コード認証が有効になったことを確認できました。
![](https://storage.googleapis.com/zenn-user-upload/88bcaac83342-20250526.png)

### 2.3 ユーザーに対して QR コード認証方法を追加する！

5. Entra 管理センターで[ユーザー]に移動し、QRコード認証を追加したいユーザーを選択し、[認証方法] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/2330d6bab684-20250527.png)

6. [認証方法の追加] で、方法の選択の項目で QRコード(プレビュー)、必要に応じて有効期限を変更し、アクティブ化の時間を今すぐに選択します。
初回サインインのみ有効な PIN を設定します。
![](https://storage.googleapis.com/zenn-user-upload/0dc4a2c12a17-20250527.png)


7. 以下の画像のように、設定した PIN と作成された QR コードが表示されます。PIN と　QR コードはユーザーにセキュアな方法で伝える必要があります。 
![](https://storage.googleapis.com/zenn-user-upload/f11af25c5bcf-20250527.png)

これで、選択したユーザーに対して、QR コード認証を有効化することができます。

### 2.4 アプリケーションに対して、QR コード認証を有効化する！
上記 2.3 までの手順ですと、Web ブラウザからのサインインに対して、QR コード認証が有効になる動作となります。
そのため、モバイルアプリにサインインする際に QR コード認証を有効にしたい場合、ひと手間加える必要があります。

8. Intune 管理センター(https://intune.microsoft.com) で [アプリ] -> [構成] -> [新しいポリシー] -> [ マネージド デバイス ] の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/7da8c83e5614-20250527.png)

9. ポリシーの確認画面で、ポリシーの名前を入力し、プラットフォームは Android Enterprise を選択し、デバイスの種類は、フル マネージド、専用、会社所有の仕事用プロファイルのみ、アプリは、Authenticator を選択します。
![](https://storage.googleapis.com/zenn-user-upload/e1a6b62171d5-20250527.png)

10. 構成設定の形式は、構成デザイナーを設定するを選択します。右のブレードが表示されますので、Preferred authentication configuration を選択し、OK をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/de201da777aa-20250527.png)

11. 構成キーの構成値を qrpin と入力し、次へをクリックします。
![](https://storage.googleapis.com/zenn-user-upload/1c339896dbf3-20250527.png)

12. 割り当てるデバイス グループを選択します。
![](https://storage.googleapis.com/zenn-user-upload/b478ad703d96-20250527.png)

13. 構成内容を確認し、作成をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/ffbe649ffbfb-20250527.png)

14. QR コード認証に対応している モバイルアプリケーションのサインイン画面に、QR コード認証が表示されます。
![](https://storage.googleapis.com/zenn-user-upload/00de026f150f-20250527.jpg)

上記手順を行っていない場合、表示されません。

### 2.5 ユーザーの初回サインインエクスペリエンスを確認する！

さて、エンドユーザー視点に立って、QR コード認証でサインインしてみます。







## 3. まとめ
今回は展開済みのクラウド PC を移動する方法をご紹介しました！
本ブログがみなさまの参考になれば幸いです😉








