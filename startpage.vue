<template id="">
  <div class="">
    
  </div>
</template>
<script type="text/javascript">
  export default{
    name: 'startpage',
    components:{
    },
    data(){
      return{
        kategorien:[
          {id: 1, text:'Männer', visible:false,
            children:[
              {id: 1, text:'T-shirts'},
              {id: 2, text:'Sweathshirt'}
          ]},
          {id: 2, text:'Frauen', visible:false, children:[
            {id: 1, text:'zeug'},
            {id: 2, text:'zeug'}
          ]},
          {id: 3, text:'Sale', visible:false, children:[
            {id: 1, text:'Neu'},
            {id: 2, text:'Summer Sale'}
          ]}
        ]
      }
    }
  }
</script>
<style media="screen">

</style>
