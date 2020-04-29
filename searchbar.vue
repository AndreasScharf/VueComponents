<template id="">
  <form>
    <input type="text" v-model="text" name="text" v-on:keyup="change" placeholder="search...">
    <input type="submit" name=""  class="search_button" v-on:click="search">
  </form>
</template>
<script type="text/javascript">
export default{
  name: 'searchbar',
  methods:{
    search(e){
      e.preventDefault();
      console.log('search', this.text);
    },
    change(){
      console.log(this.text);
    }
  },
  data(){
    return{
      text: ''
    }
  }
}
</script>
<style media="screen" scoped>
form{
  flex: 2 0 auto;
  display: flex;
  flex-direction: row;
  padding: 0 15%;
}
.search_button{
  flex: 0 0 auto;
  background-color: white;
  border: 0;
}
input{
  font-size: 20pt;
  flex: 1 0 auto;

}
</style>
