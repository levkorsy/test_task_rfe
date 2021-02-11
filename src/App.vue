<template>
  <div id="app" class="container">
    <div class="input-group mb-3">
      <input type="text" class="form-control" placeholder="Type here..." aria-label="Recipient's username"
             aria-describedby="button-addon2" v-model="hash" @keyup.13="addToHash(hash)">
      <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="addToHash(hash)">Add</button>
    </div>
    <ul class="list-group">
      <ListHashItem v-for="(hashItem, index) in listItems" :item="hashItem" :key="index" @removeItem="removeItem"/>
    </ul>

  </div>

</template>

<script>

import ListHashItem from "./components/ListHashItem";

export default {
  name: 'App',

  mounted() {
    window.location.hash = `${this.hashTitle}=red,blue,purple`
    this.getListItemsFromHash(window.location.hash)
  },
  data() {
    return {
      listItems: [],
      route: window.location.hash,
      hash: '',
      hashTitle: '#tags'

    }
  },
  components: {ListHashItem},
  methods: {
    addToHash(hash) {
      if (hash.length > 0) {
        this.listItems.push(hash)
        window.location.hash = `${this.hashTitle}=${this.listItems.join(',')}`
        this.hash =''
      }
    },
    getListItemsFromHash(hash) {
      let hashArray = hash
          .split("&")
          .map(v => v.split("="))
          .reduce((pre, [key, value]) => ({...pre, [key]: value}), {})
      this.listItems = hashArray[this.hashTitle].split(",");
    },
    removeItem(item){
      this.listItems = this.listItems.filter(listItem=> item !== listItem)
      window.location.hash = `${this.hashTitle}=${this.listItems.join(',')}`
    }
  },

  watch: {
    route: function () {
      console.log(window.location.hash.split("#/")[1])
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 30%;
  background-color: #eff2f1;
  padding: 30px;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
</style>
