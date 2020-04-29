<template id="">
  <div class="div">
    <p>{{name}}</p>
    <list class="auswahl" v-bind:items="items"/>
  </div>
</template>
<script type="text/javascript">
import list from './list.vue'
export default{
  name: 'auswahl',
  props: ['name', 'items'],
  components:{
    list
  },
  data(){
    return{

    }
  }
}
</script>
<style media="screen" scoped>
.div{
  display: flex;
  flex-direction: column;
}
p{
  flex: 0 0 auto;
  margin-bottom: 0;
}
.auswahl{
  flex: 0 0 auto;
}
</style>
