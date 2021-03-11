<template>
  <div class="simpletable">
    <list class="table header" :items="header"/>
    <div class="table_body">
      <list v-for="(row,index) in data" :key="index" :items="row" class="table body" v-on:item-clicked="$emit('row-clicked', row)"></list>
    </div>
  </div>
</template>
<script>
import list from '@/components/VueComponents/list.vue'

export default {
  name: 'simpletable',
  props: {data:Array, header:Array},
  components: { list },

}
</script>
<style>
.simpletable{
  border: solid 2pt var(--color5) ;
  border-bottom: none;
  margin: 2pt;
}
.scrollable-element {
  scrollbar-width: none;
}
.table.header{
  background-color: var(--color1);
  cursor:  default;

  border-bottom: solid 2pt var(--color5) ;

}
.table.body{
  overflow: hidden;
}
</style>