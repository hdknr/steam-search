# 作成

## 参考

- [Reactivesearchでいい感じの検索SPAを30分ぐらいで作る - Qiita](https://qiita.com/j-yama/items/546f6b7605c9e71d0454)
- [Building BookSearch Application using Vue and Elasticsearch](https://medium.appbase.io/building-booksearch-application-using-vue-and-elasticsearch-a39615f4d6b3)

## 0. サーバーの設定

- steam-search インデックスの用意
- [Reactivesearchでいい感じの検索SPAを30分ぐらいで作る - Qiita](https://qiita.com/j-yama/items/546f6b7605c9e71d0454) の手順

## 1. Vue.js プロジェクト 作成

~~~bash
$ node -v

v10.15.0
~~~

~~~bash
$ npm install -g @vue/cli
$ vue --version

3.2.3
~~~

~~~bash
$ vue create steam-search && cd steam-search
$ vue run serve

...
~~~

## 2. Reactivesearch 設定

~~~bash
$ npm add @appbaseio/reactivesearch-vue
$ npm install --save babel-runtime

...
~~~

[main.js](../src/main.js) に追加:

~~~js
import Vue from 'vue'
...
import ReactiveSearch from "@appbaseio/reactivesearch-vue"
Vue.use(ReactiveSearch)
...
~~~

## 3. SteamSearch コンポーネント

- [SteamSearch.vue](../src/components/SteamSearch.vue) を作る

~~~html
<ReactiveBase app="steam-search" url="http://192.168.56.53:9200">
    <h1>Hello from ReactiveBase ✨</h1>

    <DataSearch
        componentId="title"
        placeholder="Search..."
        :dataField="['ResponseName']"
        :queryFormat="'and'"
    />

    <ReactiveList
        componentId="resultLists"
        dataField="ResponseName"
        :size="5"
        :pagination="true"
        :react="{ and: ['title'] }"
    >

        <div slot="onData" slot-scope="{ item }">
            <div class="flex" key="item._id">
            <div class="flex column justify-center">
                <div class="response-header">{{ item.ResponseName }}</div>
            </div>
            </div>
        </div>

    </ReactiveList>

</ReactiveBase>
~~~