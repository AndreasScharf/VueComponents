<template id="">
  <div class="main_panel">
    <div class="closing-panel" v-on:mouseleave="mouseleft"></div>
    <list v-bind:items="kategorien" class="main-list" v-on:hover="hover"/>
    <div class="open-menu" v-on:mouseleave="mouseleft">
      <list v-for="item in kategorien" v-bind:key="item.id" v-bind:items="item.children" v-bind:class="{'hide':!item.visible}" class="child-list"/>
      <div class="picture" v-bind:class="{'hide':!this.child_visible}"></div>
    </div>
  </div>
</template>
<script type="text/javascript">
import list from './list.vue'
export default{
  name: 'kategorie',
  props: ['kategorien'],
  components:{
    list
  },
  methods:{
    hover(item){
    //  this.ready = true
  //    setTimeout(()=>{
    //    if(!this.ready)
      //    return;
        this.kategorien.forEach(item => item.visible = false)
        item.visible = true;
        this.child_visible = true;
        this.ready = false;
      //}, 750)
    },
    mouseleft(){
      //if(this.ready){
      //  this.ready = false;
    //    return;
    //  }
      this.ready = false;
      this.kategorien.forEach(item => item.visible = false)
      this.child_visible = false;
    }
  },
  data(){
    return{
      child_visible: false,
      ready: false

    }
  }
}
</script>
<style media="screen" scoped>
.closing-panel{
  height: 15pt;
  background-color: white;
}
.main_panel{
  background-color:#42b983;
  transition: height 0.4s;
}
.main-list{
  display: flex;
  flex-direction: row;
  color: white;
  border-bottom: solid 2pt white;
}
.main-list li{
  border-left: solid 1pt white;
  border-right: solid 1pt white;
}
.main-list li:first-child{
  border-left: none;
}
.main-list li:last-child{
  border-right: none;
}
.open-menu{
  height: auto;
  width: calc(100% - 16px);
  position: absolute;

  background-color: #42b983;
  display: flex;
  flex-direction: row;
  transition: height 0.4s;
}
.open-menu.not-show{
  height: 0;
}
.picture{
  flex: 1 0 1px;
  min-height: 250px;
  background-color: white;
}
.child-list{
  flex: 1 0 1px;
  display: flex;
  padding-bottom: 10pt;
  flex-direction: column;
  margin: auto 0;
}
.child-list li{
  text-align: left;
}
.hide{
  display: none!important;
}
</style>
<style media="screen">
.child-list li{
  text-align: left;
  padding: 10pt;
}
.main-list li{
  border-left: solid 1.25pt white;
  border-right: solid 1.25pt white;
  padding: 7.5pt 0;
}
.main-list li:first-child{
  border-left: none;
}
.main-list li:last-child{
  border-right: none;
}
</style>
