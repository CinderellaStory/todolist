<template>
  <div class="warpper">
    <h1>{{title}}</h1>
    <input v-model="NewItem" @keyup.enter="addNew" placeholder="请输入进入想做的事情~">
    <div class="item">
      <ul>
        <li v-for="(item,index) in items" :key="index" :class="{finished:item.isFined}" @click="toggleFinsh(item)">
          <!-- <i></i> -->
          <span>{{item.text}}</span>
          <em @click="del">X</em>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Store from '../store'
console.log(Store)
export default {
  name: 'HelloWorld',
  data () {
    return {
      title: '备忘录',
      NewItem:'',
      items:Store.feach()
    }
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  },
    methods:{
      toggleFinsh(item){
        item.isFined =! item.isFined
        console.log(111);
      },
      addNew(){
        this.items.push({
          text:this.NewItem,
          isFined:this.isFined
        })
        console.log(this.NewItem);
        this.NewItem = ''
      },
      del(index){
        this.items.splice(index,1);
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.warpper{
  /* border: 1px solid red; */
  width: 600px;
  margin: 0 auto;
}
h1{
  text-align: center;
  color: #fff;
  font-weight: 400;
  font-style: italic;
}
.finished{
 text-decoration:line-through;
}
input{
  outline: none;
  padding-left: 10px;
  width: 97.8%;
  height: 40px;
  font-size: 16px;
  border: 1px solid #ddd;
}
input::-webkit-input-placeholder {
      color: #aab2bd;
      font-style: italic;
      font-size: 14px;
    }
ul{
  list-style: none;
  background: #fff;
  width: 100%;
  margin: 0;
  padding: 0;
}
.item ul li{
  min-height: 40px;
  border-bottom: 1px solid #ddd;
  padding:4px 10px;
  overflow: hidden;
}
.item ul li em{
  float: right;
  color: red;
  font-size: 18px;
  cursor: pointer;
  line-height: 40px;
}
.item ul li span{
  font-size: 16px;
  line-height: 40px;
  color: #333131;
  float: left;
}
</style>
