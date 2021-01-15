# log

create:

* rails _version_ new app-name --database=postgresql

create db

* rails db:create

err!

* hasErr! rm all postgres -> re install

webpack

* rails webpacker:install
* rails webpacker:install:vue

route

* get 'home', to: 'home#index'
* rails routes

generate

* rails g controller home

app/controlllers/home_controller.rb

``` ruby
 def index
  end
```

add view

* touch app/views/home/index.html.erb
  + <%= javascript_pack_tag 'hello_vue' %>

Model

* rails g model Memo
* -> db/migrate/xxxxxx_create_memos.rb

``` ruby
    t.string :title
    t.text :description
```

* rails db:migrate

add gem

* gem 'faker'
* bundle install

Dummy Data

* db/seeds.rb

``` ruby
5.times do
  Memo.create(
    title: Faker::Lorem.word,
    description: Faker::Lorem.sentence,
  )
end
```

* rails db:seed

Check

* rails console
* Memo.all

create route

``` ruby
 namespace :api, format: 'json' do # namespace for setting path
    resources :memos, only: [:index]
  end
```

* rails routes

create  g

* rails g controller api/memos

constoller

* app/controllers/api/memos_controller.rb

``` ruby
def index
    @memos = Memo.order('created_at DESC')
end
```

jbuilder

* touch app/views/api/memos/index.json.jbuilder
* json.array! @memos, :title, :description  # (instance, key)

---

Memo:
[postgreSQL Show DB Yables command](https://qiita.com/Shitimi_613/items/bcd6a7f4134e6a8f0621)

---
