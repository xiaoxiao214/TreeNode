<template>
      <ul class="tree">
          <li class="tree-node"
            v-for="(node,index) in data "
            :key="node.label"
          >
              <i class="iconfont "
              :class="{
                  'icon-you':!showChildren[index],
                  'icon-xia':showChildren[index],
              }"
              v-if = "node.children"
              >
              </i>
              <span class="node-label"
                @click="handleClick(index)"
                >{{node.label}}</span>
                <keep-alive>
                    <base-tree :data = "node.children"
                    v-if = "showChildren[index]"/>
                </keep-alive>
          </li>
      </ul>
</template>

<script>
export default {
    name:'base-tree',
    props:{
        data:{
            type:Array,
            required:true,
        } ,
    },
    data(){
        return{
             showChildren :[]
        }
    },
    methods:{
        handleClick(index){
            const lock = !this.showChildren[index];
            this.$set(this.showChildren,index,lock);          
        }    
    },
    mounted(){

    },
}
</script>

<style>
@import "./assets/font.css";
  li{
      list-style: none;
  }
  .tree-node{
      cursor: pointer;
      font-size: 14px;
  }
  .tree-node .iconfont{
      color: #c0c4cc;
      font-size: 14px;
      margin-right: 5px;
      vertical-align: middle;

  }
  .tree-node .node-label{
      font-size: 14px;
      color: #606266;
      vertical-align: middle;
  }
  
</style>