<template>
  <div id="app">
      <select-tiles
              name="test"
              :items="items"
              v-model="selected"
              value-key="id"
              id-key="id"
              text-key="name"
              :old="[]"
              mode="checkbox"
      >
          <template slot="label">
      　　　　<span>*</span>checkbox
      　　</template>
      </select-tiles>
{{selected}}
      <select-tiles
              name="test2"
              :items="items"
              v-model="selected2"
              value-key="name"
              id-key="id"
              text-key="name"
              :old="['test1']"
              second-text-key="price"
      >
          <template slot="label">
      　　　　<span>*</span>checkbox
      　　</template>
      </select-tiles>
{{selected2}}
      <select-tiles
              name="test3"
              :items="items"
              v-model="selected3"
              value-key="name"
              id-key="id"
              text-key="name"
              :old="['test5']"
              mode="radio"
      >
          <template slot="label">
      　　    <span>*</span>radio button!!
      　　</template>
      </select-tiles>
{{selected3}}
  </div>
</template>

<script>
    import SelectTiles from './components/SelectTiles'

    export default {
        data() {
            return {
                items: [
                    {id:1, name: 'test1', price: 100},
                    {id:2, name: 'test2', price: 1000},
                    {id:3, name: 'test3',price: 10000},
                    {id:4, name: 'test4',price: 10},
                    {id:5, name: 'test5', price: 1},
                ],
                selected: [],
                selected2: [],
                selected3: []
            }
        },
        components: {
            SelectTiles,
        }
    }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.select-tiles .select-tiles__btn {
    border: 1px solid #909090;
    padding: 5px 8px;
    border-radius: 7px;
    color: #909090;
    cursor: pointer;
}

.select-tiles .select-tiles__input:checked + .select-tiles__btn {
    color: #FABD00;
    border: 1px solid #FABD00;
    background: #fff;
}
</style>
