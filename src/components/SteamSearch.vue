<template>
  <div class="steam-search">
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
  </div>
</template>

<script>
export default {
  name: 'SteamSearch',
}
</script>