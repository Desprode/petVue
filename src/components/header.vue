<template>
  <div id='header'>
    <img src="../assets/images/header/logo.jpg" alt="" class="logo">
    <el-autocomplete class="inline-input input-with-select"
      v-model="input"
      :fetch-suggestions="querySearch"
      placeholder="请输入内容"
      @select="handleSelect" 
      clearable>
      <el-button slot="append" icon="el-icon-search"></el-button>
    </el-autocomplete>
    <div class="register">
      <a>注册|</a>
      <a>登录</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      input:'',
      restaurants: [],
    }
  },
  mounted() {
      this.restaurants = this.loadAll();
  },
  methods:{
    querySearch(queryString, cb) {
        var restaurants = this.restaurants;
        var results = queryString ? restaurants.filter(this.createFilter(queryString)) : restaurants;
        // 调用 callback 返回建议列表的数据
        cb(results);
      },
      createFilter(queryString) {
        return (restaurant) => {
          return (restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) === 0);
        };
      },
      loadAll() {
        return [
          { "value": "三全鲜食（北新泾店）", "address": "长宁区新渔路144号" },
          { "value": "Hot honey 首尔炸鸡（仙霞路）", "address": "上海市长宁区淞虹路661号" },
          { "value": "新旺角茶餐厅", "address": "上海市普陀区真北路988号创邑金沙谷6号楼113" },
          { "value": "泷千家(天山西路店)", "address": "天山西路438号" },
        ]
      },
      handleSelect(item) {
        console.log(item);
      }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #header {
    display: flex;
    width:90%;
    height: 100px;
    margin:0 auto;
    justify-content: space-around;
    line-height: 100px;
  }
  #header .logo{
    width:20%;
    margin-bottom: 20px;

  }
  #header .input-with-select {
    width: 40%;
  }
  #header .register {
    width: 20%;
  } 
</style>
