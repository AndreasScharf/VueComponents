<template id="">
  <div class="background">
    <div class="left slider">

    </div>
    <div class="placeholder">
      <div class="inner-placeholder">

      </div>
      <div class="punke">
        <list/>
      </div>
    </div>
    <div class="right slider">

    </div>
  </div>
</template>
<script type="text/javascript">
  import list from './list.vue'

  export default{
    name: 'galerie',
    props: ['bilder_urls'],
    components:{
      list
    }
  }
</script>
<style media="screen">
.background{
  display: flex;
  flex-direction: row;

  height: 400px;
}
.placeholder{
  flex: 1 0 1pt;
}
.inner-placeholder{
  flex: 4 0 1pt;
}
.punke{
  flex: 1 0 1pt;
}
.slider{
  flex: 0 0 50pt;
}
</style>
