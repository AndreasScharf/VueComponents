<template id="">
  <div class="burger" v-bind:class="{'crossed':this.crossed}" v-on:click="click">
    <div class="bar1"></div>
    <div class="bar2"></div>
    <div class="bar3"></div>
  </div>
</template>
<script type="text/javascript">
  export default{
    name: 'burger',
    props: ['crossed', 'active'],
    methods:{
      click(){
        if(this.crossed)
          this.$emit('close', 1)
        else
          this.$emit('open', 1)

        if(this.active)
          this.crossed = !this.crossed;

      }
    }
  }
</script>
<style media="screen" scoped>
.font28pt.burger{
  width: 28pt;
  height: 28pt;
  margin-right: 4pt;
}
.font28pt.burger div{
  height: 4pt;
  margin-top: 4pt;
}
.font28pt.burger.crossed .bar1{
  -webkit-transform: translate(0vh, 8pt) rotate(-45deg) ;
  transform: translate(0vh, 8pt) rotate(-45deg) ;
}
.font28pt.burger.crossed .bar3{
  -webkit-transform: translate(-0vh, -8pt) rotate(45deg);
  transform: translate(-0vh, -8pt) rotate(45deg);
}

.burger{
    flex: 0 0 auto;
    cursor: pointer;

    float: right;
    width: 7vh;
    height: 7vh;
    margin-right: 1vh;
}
.burger div{
    width: 100%;
    background-color: black;
    height: 1vh;
    margin-top: 1vh;
    transition: transform 0.4s;
}
.burger.crossed .bar1{
     -webkit-transform: translate(0vh, 2vh) rotate(-45deg) ;
     transform: translate(0vh, 2vh) rotate(-45deg) ;
}
.burger .bar2{
    visibility: visible;
}
.burger.crossed .bar2{
    visibility: hidden;

}
.burger.crossed .bar3{
     -webkit-transform: translate(-0vh, -2vh) rotate(45deg);
     transform: translate(-0vh, -2vh) rotate(45deg);
}
@media  screen and (max-device-width: 800px) {
    .burger{
        display: block;
    }
}
</style>
