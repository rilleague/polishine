# README

## usersテーブル
| Column             | Type   | Options                   |
| ------------------ | ------ | ------------------------- |
| nickname           | string | null: false, unique: true |
| email              | string | null: false, unique: true |
| encrypted_password | string | null: false               |

### association
- has_many :posts
- has_many :comments
- has_many :favorites
- has_many :relationships
- has_many :followings, through: :relationships, source: :follow
- has_many :reverse_of_relationships, class_name: 'Relationship', foreign_key: 'follow_id'
- has_many :followers, through: :reverse_of_relationships, source: :user




## postsテーブル
| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| type_id            | integer    | null: false                    |
| genre_id           | integer    | null: false                    |
| title              | string     | null: false                    |
| detail             | text       | null: false                    |
| user               | references | null: false, foreign_key: true |

### association
- has_many   :favorites
- has_many   :comments
- has_many   :tags, through: :post_tags
- has_many   :post_tags
- has_many   :favorites
- belongs_to :user



## commentsテーブル
| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| content            | text       | null: false                    |
| post               | references | null: false, foreign_key: true |
| user               | references | null: false, foreign_key: true |

### association
- belongs_to :user
- belongs_to :post


## tagsテーブル
| Column             | Type       | Options                         |
| ------------------ | ---------- | ------------------------------- |
| name               | string     | null: false                     |

### association
- has_many   :posts, through: :post_tags
- has_many   :post_tags

## post_tagsテーブル
| Column             | Type       | Options                         |
| ------------------ | ---------- | ------------------------------- |
| post               | references | null: false, foreign_key: true  |
| tag                | references | null: false, foreign_key: true  |

### association
- belongs_to :post
- belongs_to :tag



## favoritesテーブル
| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| user               | references | null: false, foreign_key: true |
| post               | references | null: false, foreign_key: true |

### association
- belongs_to :user
- belongs_to :post



## relationshipsテーブル
| Column             | Type          | Options                                        |
| ------------------ | ------------- | ---------------------------------------------- |
| user               | references    | null: false, foreign_key: true, unique: true   |
| follow             | references    | null: false, foreign_key: { to_table: :users } |

### association
- belongs_to :user
- belongs_to :follow, class_name: 'User'