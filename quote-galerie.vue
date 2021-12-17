<template>
    <div class="quote-galerie">
        <quote v-for="(q, index) in quotes" :key="q.id" :quote="q.quote" :person="q.person" :class="{'show': active_index == index}"></quote>
    </div>
</template>
<script>
import quote from './quote.vue'
export default {

  name:'quote-galerie',
  props:{quotes:Array},
  components: { quote },
  data(){
      return{
          active_index:0
      }
  },
  created(){
      setInterval(() => {
          this.active_index++
          if(this.active_index >= this.quotes.length)
            this.active_index = 0
      }, 10000);
  }
}
</script>
<style >
.quote-galerie{
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: 'image';

}

.quote-galerie .quote{
  grid-area: image;

  opacity: 0;
  transition: opacity 2s;
}
.quote-galerie .quote.show{
  opacity: 1;

}
</style>