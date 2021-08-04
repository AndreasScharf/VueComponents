<template id="">
  <div class="galerie">
    <div v-for="(image,index) in images" :key="index" class="image" :class="{'show':active_index==index}" :style="`background-image:url('.${image.image}')`">
      <div class="placeholder"></div>
      <p class="inwhite">{{image.text}}</p></div>
    <div class="footer wrapper">
      <div class="placeholder"></div>
      <div class="dotwrapper">
        <div v-for="(image,index) in images" :key="index" class="dot" :class="{'show':active_index==index}" v-on:click="active_index = index"></div>
      </div>
      <div class="placeholder"></div>
    </div>
  </div>
</template>
<script type="text/javascript">

  export default{
    name: 'galerie',
    props: ['images'],
    components:{
    },
    created(){
       setInterval(()=>{
         this.active_index++;
         if(this.active_index >= this.images.length)
          this.active_index = 0;

       }, 100000)
    },
    data(){
      return{
        active_index: 0,

      }
    }
  }
</script>
<style media="screen">
.galerie .footer.wrapper{
  height: 50pt;
  margin-top: -50pt;
  display: flex;
  flex-direction: row;
}
.galerie .footer.wrapper div{
  flex: 1 0 0;
}
.galerie .footer.wrapper .dotwrapper{
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  z-index: 10;
}
.galerie .footer.wrapper .dot{

  border-radius: 50%;
  background-color: rgba(255, 255, 255 , 0.5);
  width: 30pt;
  flex: 0 0 auto;
  height: 30pt;
  margin: auto 15pt;
  cursor: pointer;

}
.galerie .footer.wrapper .dot.show{
  background-color: rgba(255, 255, 255 , 0.8);
}
.galerie{
  height: 600pt;

  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: 'image';
}
.galerie .image{
  grid-area: image;
  flex: 1 0 0;

  background-position: center;
  background-repeat: no-repeat;
  background-size: 100%;
  opacity: 0;
  transition: opacity 2s;
}
.galerie .image.show{
  opacity: 1;

}
p.inwhite{
  font-size: 22pt;
  line-height: 22pt;
  font-weight: bold;
  background-color: rgba(255,255,255,0.8);
  margin-bottom: 100pt;
  padding-left: 60pt;
  padding-top: 20pt;
  padding-bottom: 20pt;
  width: 350pt;
  display: inline;
  color: rgba(0,0,0, 0.5);
}
.galerie .image{
  display: flex;
  flex-direction: column;

}
.galerie .image .placeholder{
  flex: 1 0 0;
}
</style>
