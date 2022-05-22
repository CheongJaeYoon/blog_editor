<template>
<div class="menu">
    <div v-for="(obj, name) in category"
    :key="name"
    :class="name + ' ' + 'depth1'">
        <div class="depth1 box">
            <span class="name">{{ name }}</span>
        </div>

        <div v-for="(subobj, subname) in obj"
        :key="subname"
        @click="depth2click(name, subobj)"
        :class="subobj.postname + ' ' + 'depth2 hidden'">
            {{subobj.postname}}
        </div>
    </div>
    <div @click="clickedExportButton" class="export">내보내기</div>
</div>
</template>
<script>
const fs = require("fs");
//import post from '@/assets/post.json'
export default {
  name: 'SideMenu',
  data () {
    return {
      category: {},
      click:{}
    }
  },
  methods: {
    depth2click(str, obj){
      this.$store.state.currentPost = str+'/'+obj.postname;
    },
    clickedExportButton(){
      console.log(fs)
    }
  },
  created(){
    this.category = require('@/assets/post.json');
//    console.log(JSON.parse(JSON.stringify(this.category)))
    for(let key in this.category){
      console.log(key)
    }
  },
  mounted(){
  }
}
</script>
<style scoped>
  .menu{
    height: 100%;
    width: 100%;
    background-color: whitesmoke;
  }
  .depth1{
    cursor: pointer;
    font-size: 30px;
    text-align: left;
    padding-top: 30px;
  }
  .depth1.box{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
  }
  .depth1 .name{
      padding-left: 20px;
  }
  .depth2{
    cursor: pointer;
    font-size: 15px;
    text-align: left;
    padding-left: 40px;
    padding-top: 5px;
  }
  .depth2:hover{
      background-color: #aaa;
  }
</style>