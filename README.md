# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...


# テーブル設計

## usersテーブル

| Column                |  Type      |  Options                   |
|-----------------------|------------|----------------------------|
| name                  | string     | null: false                |
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