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
Entra ID の認証方法として、QR コード認証がプレビューされました！現時点では、Android, iOS, iPadOS の**共有デバイス**に対応しています。
フロントライン ワーカーの抱える課題として、サインインする際に、ユーザー名とパスワードを入力する手間があります。
以下の公開情報にも記載のように、フロントライン ワーカーに対して、QR コード認証はシンプルな認証方法を提供します。条件付きアクセスや Intune との連携により、QR コード認証方法を準拠済み共有デバイスのみに制限するポリシーを作成することもできます。


公開情報：[ Simplify frontline workers’ sign-in experience with QR code authentication ](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/simplify-frontline-workers%E2%80%99-sign-in-experience-with-qr-code-authentication/3822034)


:::message
ポイント QR コード認証は、QR コードスキャンと PIN の入力のみでサインインが可能です。
:::


## 2.試してみる！

### 2.1 構成の説明
1. 今回は Entra ID の共有デバイス モードの Android デバイスで、QR コード認証を試してみます。


### 2.2 QR コード認証方法を有効化する！


以下の公開情報に沿って検証してみます。細かい前提条件を確認されたい場合、以下の公開情報が参考になります。
#### 公開情報：[ Microsoft Entra ID の認証方法 - QR コード認証方法 (プレビュー) ](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/simplify-frontline-workers%E2%80%99-sign-in-experience-with-qr-code-authentication/3822034)

1. 少なくとも認証ポリシー管理者以上で Entra 管理センター (https://entra.microsoft.com) にアクセスします。
左のブレードの [保護] -> [認証方法] -> [QR コード認証 (プレビュー)] の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0440a92022f3-20250526.png)


2. QR コード認証の設定画面が表示されます。この表示画面では、QR コード認証の有効化と有効化するグループ選択します。
今回は、FLW というグループを選択しました。次に構成をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/2257562b6e5a-20250526.png)


3. この画面では、QR コード認証で利用する PIN の長さ ( 8 桁以上 20 桁以下 ) と QR コードの有効期限 ( 1 日以上 395 日以下) の設定ができます。今回は既定 ( 365 日) のまま進みます。
![](https://storage.googleapis.com/zenn-user-upload/9dfea5e545a7-20250526.png)


4. QR コード認証が有効になったことを確認できました。
![](https://storage.googleapis.com/zenn-user-upload/88bcaac83342-20250526.png)

### 2.3 ユーザーに対して QR コード認証方法を追加する！

5. Entra 管理センターで [ユーザー] に移動し、QR コード認証を有効にしたいユーザーを選択し、[認証方法] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/2330d6bab684-20250527.png)

6. [認証方法の追加] で、方法の選択の項目で QR コード(プレビュー)、必要に応じて有効期限を変更し、アクティブ化の時間を今すぐに選択します。
初回サインインのみ有効な PIN を設定します。
![](https://storage.googleapis.com/zenn-user-upload/0dc4a2c12a17-20250527.png)


7. 以下の画像のように、設定した PIN と作成された QR コードが表示されます。PIN と　QR コードはユーザーにセキュアな方法で伝える必要があります。 
![](https://storage.googleapis.com/zenn-user-upload/f11af25c5bcf-20250527.png)

これで、選択したユーザーに対して、QR コード認証を有効化することができます。

### 2.4 QR コードを使用して、Microsoft Microsoft Teams にサインインする！
上記 2.3 までの手順ですと、Web サインインに対して、QR コード認証が有効になる動作となります。
Microsoft Teams, Managed Home Screen には、最適化された QR コード サインイン エクスペリエンスがあります。
そのための設定を Intune から行います。

1. Intune 管理センター(https://intune.microsoft.com) で [アプリ] -> [構成] -> [新しいポリシー] -> [マネージド デバイス] の順にクリックします。
![](https://storage.googleapis.com/zenn-user-upload/7da8c83e5614-20250527.png)

2. ポリシーの確認画面で、ポリシーの名前を入力し、プラットフォームは Android Enterprise を選択し、デバイスの種類は、"フル マネージド、専用、会社所有の仕事用プロファイルのみ" 、アプリは、Authenticator を選択します。
![](https://storage.googleapis.com/zenn-user-upload/e1a6b62171d5-20250527.png)

3. 構成設定の形式は、[構成デザイナーを設定する] を選択します。右のブレードが表示されますので、Preferred authentication configuration を選択し、[OK] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/de201da777aa-20250527.png)

4. 構成キーの構成値を qrpin と入力し、[次へ] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/1c339896dbf3-20250527.png)

5. 割り当てるデバイス グループを選択します。
![](https://storage.googleapis.com/zenn-user-upload/b478ad703d96-20250527.png)

6. 構成内容を確認し、[作成] をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/ffbe649ffbfb-20250527.png)

7. QR コード認証に対応している モバイルアプリケーションのサインイン画面に、QR コード認証が表示されます。
![](https://storage.googleapis.com/zenn-user-upload/00de026f150f-20250527.jpg)

上記手順を行っていない場合、以下のように表示されません。
![](https://storage.googleapis.com/zenn-user-upload/b51087e2d8ad-20250528.jpg)



### 2.5 ユーザーの初回サインイン エクスペリエンスを確認する！

さて、エンド ユーザー視点に立って、モバイル アプリの Teams に QR コード認証でサインインしてみます。

1. Sign in with a QR code をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/00de026f150f-20250527.jpg)

2. QR コードをスキャンします。
![](https://storage.googleapis.com/zenn-user-upload/42b81499862a-20250528.jpg)

3. QR コードの PIN を入力します。 
![](https://storage.googleapis.com/zenn-user-upload/9058d90c9bef-20250528.jpg)

4. サインインできました！
![](https://storage.googleapis.com/zenn-user-upload/eca410790795-20250528.jpg)

※初回サインインは、PIN の再設定を行った後サインインする動作となります。

細かい条件や動作を確認されたい方は、以下の公開情報が参考になると思います。

[Microsoft Entra ID の認証方法 - QR コード認証方法 (プレビュー)](https://learn.microsoft.com/ja-jp/entra/identity/authentication/concept-authentication-qr-code)
[Microsoft Entra ID で QR コード認証方法を有効にする方法 (プレビュー)](https://learn.microsoft.com/ja-jp/entra/identity/authentication/how-to-authentication-qr-code)



## 3. まとめ
今回は プレビュー中の QR コード認証を試してみました！QR コードのスキャンと PIN の入力のみでサインインできるのは魅力的ですね。個人的に Windows の共有端末でも使えるようになればもっと良いと思いました。今後に期待ですね！
本ブログがみなさまの参考になれば幸いです😉








