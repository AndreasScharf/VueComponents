<template id="app">
  <div class="">
    <kategories v-bind:kategorien="this.kategorien"/>
    <div class="produkt">
      <galerie class="galerie"/>
      <div class="sidebar">
        <p>Produkt</p>
        <div class="produkt-beschreibung">
          <auswahl name="Größe" v-bind:items="groeßen"/>
          <auswahl name="Farbe" v-bind:items="farben"/>

          <div class="einkaufswagen">

            <input type="number" value="1" v-model="menge">
            <button type="button" name="button" v-on:click="inEinkaufswagen"><img color="white" src="../assets/shopping-cart-white.svg"/> In den Einkaufswagen</button>
          </div>

          <p>Produktbeschreibung:</p>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </div>
      </div>
    </div>
  </div>
</template>
<script type="text/javascript">
import kategories from './kategories.vue'
import galerie from './galerie.vue'
import auswahl from './auswahl.vue'
  export default{
    name: 'products',
    components:{
      kategories,
      galerie,
      auswahl
    },
    methods:{
      inEinkaufswagen(){
        let groeße = this.groeßen.filter(item => item.active)[0].text;
        let farbe = this.farben.filter(item => item.active)[0].text;
        console.log('Produkt' + this.menge + ' Größe:' + groeße + ' Farbe:' + farbe);
        let token = localStorage.getItem('token');
        if(!token){
          return;
        }
        this.$emit('in-Einkaufswagen', 1)

      }
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
        ],
        groeßen:[
          {id:1, text:'XS', active:false},
          {id:2, text:'S', active:false},
          {id:3, text:'M', active:true},
          {id:4, text:'L', active:false},
          {id:5, text:'XL', active:false},
          {id:6, text:'XXL', active:false}
        ],
        farben:[
          {id:1, text:'rot', active:true},
          {id:2, text:'grün', active:false},
          {id:3, text:'blau', active:false},
          {id:4, text:'schwarz', active:false}
        ],
        menge: 1

      }
    }
  }
</script>
<style media="screen" scoped>
p{
  text-align: left;
  margin-bottom: 2pt;
}
a{
  margin-top: 20pt;
}
input{
  flex: 0 0 auto;
  margin-left: 10pt;
  display: block;
  font-size: 20pt;
  margin: auto 0;
  margin-left: 10pt;
  margin-right: 20pt;
  width: 60pt;
}
.header, .main, .footer{
  height: 300px;
}
.header{
  background-color: #42b983;
}
.footer{
  background-color: #2c3e50;
}
.produkt{
  flex: 1 0 auto;
  display: flex;
  flex-direction: row;
}
.galerie{
  flex: 2 0 1pt;
}
.sidebar{
  flex: 3 0 1pt;
}
.produkt-beschreibung{
  text-align: left;
}
.einkaufswagen{
  display: flex;
  flex-direction: row;
  padding: 10pt 0;
}
button{
  display: flex;
  flex-direction: row;
}
button img{
 flex: 1 0 1pt;
 height: 22pt;
 color: white;
}
</style>
