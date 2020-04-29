<template id="">
  <div class="">
    <table ref="table">
      <th v-bind:value="this.table.header">
        <tr v-for="head in this.table.header" v-bind:key="head.id" v-bind:class="head.class">{{head.text}}</tr>
      </th>

      <td v-for="(row, x_index) in this.table.data" v-bind:key="row.id">
        <tr v-for="(cell, y_index) in row.data" v-bind:key="cell.id" v-bind:class="cell.class" v-on:click="click(cell, x_index, y_index)">
          <a v-bind:class="{'hide':cell.edit}">{{cell.text}}</a>
          <input ref="input" v-bind:class="{'hide':!cell.edit}" type="text" v-model="cell.text"  v-on:keyup.enter="enter">
        </tr>
      </td>
    </table>
  </div>
</template>
<script type="text/javascript">
export default{
  name: 'datatable',
  props: ['table'],
  methods:{
    click(cell, x_index, y_index){
      if (cell.click)
        cell.click(cell)
      this.table.data.forEach((row) => {
        if(row.data)
          row.data.forEach((item) =>{
            if (item.edit){
              item.edit = false
            }
          });
      });

      cell.edit = !(cell.edit == undefined);

      const length = this.table.data[0].data.length;
      this.open_input_index = x_index * length  + y_index;


    },
    enter(){
      this.table.data.forEach(row => {
        if(row.data)
          row.data.forEach(item =>{
            if (item.edit)
              item.edit = false });
      });
      this.$emit('data-changed');
    }
  },
  data(){
    return{
      open_input_index: -1
    }
  },
  updated(){
    this.$nextTick(()=> {
      if(this.open_input_index < 0)
        return;

    this.$refs.input[this.open_input_index].focus();
    });
  }

}
</script>
<style media="screen">
.hide{
  display: none !important;
}
input{
  font-size: 18pt;
}
</style>
