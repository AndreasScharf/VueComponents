<template>
  <div ref="article" class="article-with-images" :class="{'right':layout? layout.right: false}" :style="`height:${(layout && layout.height)? layout.height + 'px':'auto'}`">
    <div class="content" v-html="`<div class='placeholder'></div> ${content} <div class='placeholder'></div>`"></div>
    <div class="icon image" :style="`background-image: url('${(image && image.image)? image.image: ''}'; background-position-y: ${image_position()}px; opacity: ${image_opacity()}`" ></div>

  </div>
</template>
<script>
export default {
  name: 'article-with-image',
  props: { content:String, image: Object, layout:Object},
  methods:{
    handlescroll(){
      this.scrollPosition = window.scrollY
      if(!this.$refs.article)
        return;
      let mytop = this.$refs.article.getBoundingClientRect().top
      let absolut_top = mytop + this.scrollPosition
      this.scrollYper = (1-mytop/absolut_top) < 1? (1-mytop/absolut_top): 1;
    }
  },
  data(){
    return{
      scrollPosition:0,
      scrollYper: 0,
      image_position() {return (this.image && this.image.animation)? (1 - (this.scrollYper + 0.3 < 1? this.scrollYper + 0.3:1)) * this.layout.height: 0},
      image_opacity() {return (this.image && this.image.animation)? this.scrollYper: 1},

    }
  },
  mounted(){
    window.addEventListener('scroll', this.handlescroll);
  },destroyed(){
    window.removeEventListener('scroll', this.handlescroll);
  }
}
</script>
<style>
.article-with-images{
  display: flex;
  flex-direction: row;

  margin: 20pt 5% ;
}
.article-with-images.right{
  flex-direction: row-reverse;
}
.article-with-images .content{
  flex: 4 0 0;
  
  display: flex;
  flex-direction: column;
}
.article-with-images .content p{
  flex: 0 0 auto;
  text-align: left;
  font-size: var(--font2);
  margin-bottom: 5pt;
}
.article-with-images .content div{
  text-align: left;
  font-size: var(--font1);

}
.article-with-images .image{
  flex: 1 0 0;
}
.article-with-images .placeholder{
  flex: 1 0 0;
}
</style>