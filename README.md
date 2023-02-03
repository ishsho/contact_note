# アプリケーション名
ContactNote
<br />
<br />

# アプリケーション概要
定期的に更新される伝達事項の共有をスムーズに行うことができる。
<br />
<br />

# URL

<br />
<br />

# テスト用アカウント
・ Basic認証ID : ishsho  
・ Basic認証パスワード : 1203  
・ ログインパスワード : 111111
<br />
<br />

# 利用方法
トピックスの閲覧及び投稿
---  
___
1.URLに遷移するとログイン画面が表示される。  
2.トピックスの下にある新規作成ボタンから、新しいトピックスを作成する。  
3.  

<br />

項目の閲覧及び投稿
---
___
1.  
2.  
3.  
<br />

# アプリケーションを作成した背景
自分自身をペルソナにし、前職での社内における様々な伝達事項の共有方法が、非常に不便でストレスを感じた経験があったことが判明した。  方法としては社内メールにて伝達事項が記載されたPDFを全社員に一斉送信するというものだったが、メールやPDFのタイトルづけも曖昧で、確認の度に一つ一つPDFを開いて探す必要があった。  
そこでストレスなく今までに発信された伝達事項を手早く確認できるアプリケーションを開発することにした。
<br />
<br />

# 洗い出した要件
[要件を定義したシート](https://docs.google.com/spreadsheets/d/1hPcdfzZ0Nhv3sjtiWoG7QFnbUg65fBB31BzNE2ETZWc/edit#gid=982722306)
<br />
<br />

# 実装した機能についての画像やGIFおよびその説明

<br />
<br />

# 実装予定の機能
複数人で行えるチャット機能の実装
<br />
<br />

# データベース設計
[![Image from Gyazo](https://i.gyazo.com/6cffebd7363b985d851c1a9f1491eddd.png)](https://gyazo.com/6cffebd7363b985d851c1a9f1491eddd)
<br />
<br />

# 開発環境
・ Ruby/Ruby on Rails/MySQL/Github/Visual Studio Code
<br />
<br />

# 工夫したポイント

<br />
<br />


# テーブル設計

## usersテーブル

| Column                |  Type      |  Options                   |
|-----------------------|------------|----------------------------|
| name                  | string     | null: false                |
| email                 | string     | null: false                |
| encrypted_password    | string     | null: false                |


### Association

- has_many :topics
- has_many :room_users
- has_many :rooms, through: :room_users
- has_many :messages



## topicsテーブル

| Column                |  Type      |  Options                       |
|-----------------------|------------|--------------------------------|
| title_name            | string     | null: false                    |
| user                  | references | null: false, foreign_key: true |


### Association

- has_many   :contents
- belongs_to :user



## contentsテーブル

| Column                |  Type      |  Options                       |
|-----------------------|------------|--------------------------------|
| content_title         | string     | null: false                    |
| content               | text       | null: false                    |
| topic                 | references | null: false, foreign_key: true |


### Association

- belongs_to :topic



## room_usersテーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| room   | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user



## rooms テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |

### Association

- has_many :room_users
- has_many :users, through: :room_users
- has_many :messages