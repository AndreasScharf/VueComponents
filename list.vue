<template>
    <ul v-on:mouseleave="$emit('mouseleave')">
        <li class="list" v-for="item of items" v-bind:value="item" v-bind:key="item.id" v-bind:class="{'active':item.active, 'hide':item.hide}" 
        v-on:click="click(item)" @mouseover="hover(item)" >
            {{item.text}}
        </li>
    </ul>
</template>
<script type="text/javascript">
  export default{
    name:'list',
    props:['items'],
    components:{

    },
    methods:{
      click(item){
      this.items.forEach( item => item.active = false );
        item.active = true;

        if(item.click)
          item.click(item);
          else if(item.both_events){
            item.click(item);
            this.$emit('item-clicked', item)
          }else
          this.$emit('item-clicked', item)

      },
      hover(e){
        this.$emit('hover', e)
      }
    },
    created(){

    }

  }
</script>
<style media="screen" scoped>
    ul{
        display: flex;
        margin: 0;
        padding: 0;
    }
    li{
        flex: 1 0 auto;
        list-style-type: none;
        cursor: pointer;
        padding: 0;
    }
    ul.navbar{
        flex-direction: row;
    }
    ul.navbar li{
        flex: 1 0 0;
        text-align: center;
        border-bottom: solid 2pt transparent;
    }
    ul.navbar li.active{
        border-color: var(--color2);
    }
    ul.sidebar{
      flex-direction: column;
      overflow-y: scroll;
      max-height: calc(100vh - (5vh + 88pt));

    }
    ul.sidebar li{
        flex: 0 0 auto;
        text-align: left;
        background-color: white;
        color: #2c3e50;
        padding: 0 15pt;
    }
    ul.sidebar li.active{
        color: white;
        background-color: var(--color2);
    }
    ul.auswahl{
      flex-direction: row;
      flex: 0 0 auto;
    }
    ul.auswahl li{
      margin: 0 10pt;
      flex: 1 0 auto;
      border: solid 2pt #2c3e50;
      color: #2c3e50;
      padding: auto;
      text-align: center;
    }
    ul.auswahl li.active{
      border-color: var(--color2);
    }
    ul.vertical{
      display: flex;
      flex-direction: column;
    }
    ul.vertical li{
      text-align: left;
      padding: 10pt;
    }

    ul.table{
      display: flex;
      flex-direction: row;

     background-color: var(--color1);
    }
    ul.table li{
      flex: 1 0 0;
    }
    ul.table li.hide{
      display: hide;
    }
    ul.table.header{
     overflow: hidden;
    }
    ul.table li{
      padding: 5pt;
      text-align: left;

      border-bottom: solid 2pt var(--color5) ;

    }
    ul.table.header li{
      color: var(--color6);
      font-weight: bold;
      border-bottom: none;

    }

  
</style>
