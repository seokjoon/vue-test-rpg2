<template>
  <div id="app">

    <input type="text" v-model="item.title" />
    <br />
    <input type="text" v-model="item.content" />
    <br />
    <button @click="createItem">create</button>
    <br />
    <input type="text" v-model="itemId">
    <button @click="deleteItem">delete</button>
    <button @click="updateItem">update</button>

    <div>
      <button @click="readItems">readsItems</button>
<!--      {{ items }}-->
      <div v-for="item in items" :key="item.id" :item="item">
        {{ item.id }} || {{ item.title }} || {{ item.content }}
      </div>
    </div>

  </div>
</template>



<script>
import axios from 'axios'

const URL_API_FOO = 'http://localhost/api/foos'

export default {
  name: 'App',

  data() {
    return {
      item: {
        id: 0,
        content: '',
        title: '',
      },
      itemId: 0,
      items: [],
    }
  },


  methods: {
    async createItem() {
      const res = await axios.post(URL_API_FOO, { ...this.item })
      console.log(res)
    },

    async deleteItem() {
      const res = await axios.delete(URL_API_FOO + '/' + this.itemId)
      console.log(res.data)
    },

    async readItems() {
      const res = await axios.get(URL_API_FOO)
      this.items = res.data
      console.log(res)
    },

    async updateItem() {
      const res = await axios.put(URL_API_FOO + '/' + this.itemId, { ...this.item })
      console.log(res)
    },
  },


  watch: {
    'item': {
      deep: true,
      handler() {
        console.log('watch', this.item)
      },
    },
  },
}
</script>



<style>

</style>
