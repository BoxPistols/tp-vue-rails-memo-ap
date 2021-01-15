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

Auto Reload:

* bin/webpack-dev-server

---

Axis: MemoList

* yarn add axios

app/javascript/app.vue

``` html
<ul>
    <li v-for="memo in memos" :key="memo.id">
        {{ memo.title }}： {{ memo.description }}
    </li>
</ul>
```

``` js
// js
import axios from 'axios';
...
mounted() {
        this.setMemo();
    },
    methods: {
        setMemo: function() {
            axios.get('/api/memos')
                .then(response => (
                    this.memos = response.data
                ))
        }
    }
```

API  Test：

1. create action
1. jbuilder return json
1. Talend API Tester 

routes.rb

* resources :memos, only: [:index, :create]

create Action

* app/controllers/api/memos_controller.rb

``` ruby
 def create
    @memo = Memo.new(memo_params) #instance(call post_params)
    if @memo.save # do save insance
      render :show, status: :created # move if succsess / add status
    else
      render json: @memo.errors, status: :unprocessable_entity
    end
  end

  private # impossible call outer
    def memo_params #(post_params)
      params.permit(:title, :description) # params = request-info / params(possible change keys)
    end
```

return json on jbuilder

* touch app/views/api/memos/show.json.jbuilder

``` js
json.title @memo.title
json.description @memo.description
```

API Test

* Talend API Tester
* Post
* api/memos

add body

``` json
{
  "title": "メモのタイトル",
  "description": "メモの詳細"
}
```

* 422 Unprocessable Entity

CSRF（Cross-Site Request Forgery）

* off
* app/controllers/application_controller.rb
* protect_from_forgery

Post Memo:
