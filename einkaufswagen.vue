<template id="">
  <div class="einkaufswagen">
    <div class="placeholder" v-on:click="click"></div>
    <div class="menge" v-on:click="click">{{(items.length == 0)? '': items.length}}</div>
    <div class="menu" v-bind:class="{'hide':!this.visible}">
      <div class="wrapper">
        <div class="placeholder"></div>
        <burger class="burger font28pt" crossed="true" v-on:close="close"></burger>
      </div>
      <list class="vertical" v-bind:items="items"/>
      <button type="button" name="button" v-on:click="zurKasse">Zur Kasse</button>
    </div>
  </div>

</template>
<script type="text/javascript">
  import burger from './burger.vue'
  import list from './list.vue'
  export default{
    name: 'einkaufswagen',
    props:['items'],
    components:{
      burger,
      list
    },
    methods:{
      click(){
        this.visible = !this.visible;
      },
      close(){
        this.visible = false;
      },
      zurKasse(){
        console.log('test');
      }

    }, data(){
      return{
        visible:false
      }
    }
  }
</script>
<style media="screen" scoped>
.einkaufswagen{
  flex: 0 0 32pt;
  display: flex;
  flex-direction: column;

  background-size: contain;
  background-image: url('../assets/shopping-cart-black.svg');
  background-repeat: no-repeat;
  background-position: center;
}
.wrapper{
  display: flex;
  flex-direction: row;
}
.placeholder{
  flex: 1 0 1pt;
  cursor: pointer;

}
.menge{
  cursor: pointer;

  flex: 0 0 auto;
  margin-left: 26pt;
  font-weight: bold;
  background-color: #42b983;
  width: 23pt;
  border-radius: 12pt;
}
.einkaufswagen .menu{
  position: absolute;
  width: 300pt;
  height: auto;
  background-color: white;
  top: 50pt;
  margin-left: -125pt;
  z-index:10;
  display: flex;
  flex-direction: column;
  box-shadow: grey 0pt 5pt 5pt 3pt;

}
.hide{
  display: none !important;
}
button{
  margin: 0 5pt;
  margin-bottom: 5pt;
}
</style>
