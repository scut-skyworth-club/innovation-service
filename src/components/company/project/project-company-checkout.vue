<template>
  <div id="company-project-checkout" v-if="items.length!==0">
    <p class="company-project-guide"><router-link to="/project/company" class="router-link">项目></router-link>我的项目</p>
    <i class="last-page" v-on:click="pageReduce"><img src="../../../assets/images/向左.png"/></i>
    <ul class="company-project-items">
      <li class="company-project-item" v-for="(item,index) in items" :key="index" v-show="(index<page*4)&&(index>=page*4-4)">
            <router-link v-if="item.proState===0" :to="{path:'/'}" class="company-project-item-container">
                <img class="company-project-item-image" src="../../../assets/images/未发布.png">
                <p class="company-project-item-message-1">项目尚未发布</p>
                <p class="company-project-item-message-1">点击进行编辑</p>
            </router-link>
            <router-link v-else-if="item.proState===1" :to="{path:'/'}" class="company-project-item-container">
              <img class="company-project-item-image" src="../../../assets/images/已发布.png">
              <p class="company-project-item-message-2">项目已发布</p>
              <p class="company-project-item-message-2">共有<span class="company-project-item-people">24</span>人投递简历</p>
            </router-link>
            <router-link v-else-if="item.proState===2" :to="{path:'/project/stage',query:{proName:item.proName}}" class="company-project-item-container">
              <img class="company-project-item-image" src="../../../assets/images/进行中.png">
              <p class="company-project-item-message-3">项目进行中</p>
            </router-link>
            <router-link  v-else-if="item.proState===3" :to="{path:'/project/stage',query:{proName:item.proName}}"  class="company-project-item-container">
              <img class="company-project-item-image" src="../../../assets/images/已完成.png">
              <p class="company-project-item-message-4">项目已完成</p>
            </router-link>

      </li>
    </ul>
    <i class="next-page" v-on:click="pagePlus"><img src="../../../assets/images/向右.png"/></i>
    <p class="count-page">{{page}}/{{pageCount}}</p>
  </div>
  <div v-else id="company-no-project">
    <p class="company-no-project-guide"><router-link to="/project/company" class="router-link">项目></router-link>我的项目</p>
    <p class="company-no-project-p">您还没有任何项目</p>
    <router-link to="/" class="company-no-project-a">现在创建一个？</router-link>
  </div>
</template>

<script>
export default {
  data () {
    return {
      page: 1,
      items:[ // 待更新的数据
        {
          "proId": 0,
          "proName": '第一个项目',
          "proMoney": 1000,
          "proType": 'typeA',
          "companyName": 'companyA',
          "proCycle": 37,
          "pubTime": 1,
          "proDescription": "description",
          "proRequest": "request",
          "proState": 0
        },
        {"proId":1,"proName": '第一个项目',"proState": 1},
        {"proId":2,"proName": '第一个项目',"proState": 2},
        {"proId":3,"proName": '第二个项目',"proState": 3},
        {"proId":4,"proState": 1},
        {"proId":5,"proState": 0},
        {"proId":6,"proState": 3},
        {"proId":7,"proState": 1},
        {"proId":8,"proState": 2},
        {"proId":9,"proState": 3}
      ]
    }
  },
  computed:{
    pageCount: function() {
      return Math.ceil(this.items.length/4)
    }
    
  },
  methods: {
    pagePlus: function() {
      if(this.page!==this.pageCount) {
        this.page++
      }
    },
    pageReduce: function() {
      if(this.page!==1) {
        this.page--
      }
    }
  }
}
</script>

<style scoped>
#company-project-checkout {
  display: grid;
  grid-template-rows: 40px 50px 800px 30px;
  grid-template-columns: 23px 56px 1fr 56px 23px;
  background: #eee;
  min-height: 100vh;
}
.company-project-guide {
  font-size: 18px;
  color: #777;
  grid-area: 2/2/3/6;
  margin-left:50px;
}
.company-project-guide .router-link{
  text-decoration: none;
  color: #777;
}
.last-page {
  grid-area: 3/2/4/3;
  align-self: center;
  justify-self: start;
  cursor: pointer;
}
.next-page {
  grid-area: 3/4/4/5;
  align-self: center;
  justify-self: end;
  cursor: pointer;
}
.company-project-items {
  grid-area: 3/3/4/4;
}
.count-page {
  grid-area: 5/3/6/4;
  justify-self: center;
  color: #777;
}
.company-project-items {
  list-style: none;
  grid-area: 3/3/4/4;
  display: grid;
  grid-auto-flow: column;
  grid-template-columns: 1fr 33px 1fr 33px 1fr 33px 1fr;
}
.company-project-item {
  background-color: #fff;
  align-self: stretch;
  display: grid;
  align-items: center;
  justify-items: center;
}
.company-project-item:nth-child(4n+1) {
  grid-column: 1/2;
}
.company-project-item:nth-child(4n+2) {
  grid-column: 3/4;
}
.company-project-item:nth-child(4n+3) {
  grid-column: 5/6;
}
.company-project-item:nth-child(4n) {
  grid-column: 7/8;
}
.company-project-item-container {
  display: grid;
  align-items: start;
  justify-items: center;
  grid-template-rows: 177px 50px 33px;
  text-decoration: none;
}
.company-project-item-people {
  color: #3f88fc;
}
.company-project-item-message-1 {
  color: #eee;
  font-size: 25px;
}
.company-project-item-message-2 {
  color: #ccc;
  font-size: 25px;
}
.company-project-item-message-3 {
  color: #999;
  font-size: 25px;
}
.company-project-item-message-4 {
  color: #444;
  font-size: 25px;
}
/*没有项目*/
#company-no-project {
  display: grid;
  background: #eee;
  min-height: 100vh;
  grid-template-rows: 40px 398px 42px;
}
.company-no-project-guide {
  font-size: 18px;
  color: #777;
  grid-row: 2/3;
  margin-left:50px;
}
.company-no-project-guide .router-link {
  text-decoration: none;
  color: #777;
}
.company-no-project-p {
  grid-row: 3/4;
  font-size: 24px;
  justify-self: center;
  align-self: start;
  color: #777;
}
.company-no-project-a {
  grid-row: 4/5;
  font-size: 24px;
  justify-self: center;
  align-self: start;
  color: #3f88fc;
}
</style>


