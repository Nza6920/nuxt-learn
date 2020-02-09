<template>
    <div class="page">
      创建即配置
      <ul>
        <li v-for="(item, idx) in $store.state.navbar.app" :key="idx">
            {{ item }}
        </li>
      </ul>
    </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'search',
    layout: 'search',   // 使用模板
    data() {
      return {
        list: []
      }
    },
    async asyncData() {  // fetch 处理 vuex , asyncData 处理组件数据
      let {status, data: {list}} = await axios.get('http://localhost:3000/city/list')
      if (status === 200) {
        return {
          list
        }
      }
    },
    async fetch({store}) {  // fetch 处理 vuex , asyncData 处理组件数据
      let {status, data: {list}} = await axios.get('http://localhost:3000/city/list')
      if (status === 200) {
        store.dispatch('navbar/add', list[0])
      }
    }
  }
</script>

<style scoped>


</style>
