<template>
  <div id="main_div">
    <div class="toLogin" v-bind:class="{'hide':this.open_at_start}">
      <input type="button" value="Sign In" v-on:click="open(0)" class="opener button">
      <input type="button" value="Sign Up" v-on:click="open(1)" class="opener button">
    </div>
    <div class="user" v-bind:class="{'hide':true}">

    </div>
    <div class="background" v-bind:class="{'hide':!(this.visible || this.open_at_start)}">
        <div class="">
            <list class="navbar" v-bind:items="items"/>
            <form>
                <!--Login item 0 Register item 1-->
                <div class="wrapper" v-bind:class="{'hide': !items[1].active}">
                    <label for="">
                        <p>Vorname:</p>
                        <input type="text" v-model="name">
                    </label>
                    <label for="">
                        <p>Nachname:</p>
                        <input type="text" v-model="lastname">
                    </label>
                </div>

                <label>
                    <p>E-mail:</p>
                    <input type="text" v-model="email">
                </label>
                <label>
                    <p>Passwort:</p>
                    <input type="password" v-model="password">
                </label>

                <label class="checkbox" v-bind:class="{'hide': !items[0].active}">
                    <checkbox class="font-20pt" v-model="remain_signed_in" text="Angemeldet bleiben"/>
                </label>

                <label v-bind:class="{'hide': !items[1].active}">
                    <p>Passwort wiederholden:</p>
                    <input type="password" v-model="password_again">
                </label>

                <license v-bind:class="{'hide': !items[1].active}" pre_text="Ich stimme den " open_text="Lizensvereinbarungen" post_text=" zu" v-bind:license_text="lvb_text"/>
                <license v-bind:class="{'hide': !items[1].active}" pre_text="Ich stimme den " open_text="AGBs" post_text=" zu" v-bind:license_text="agb_text"/>
                <div class="wrapper btn">
                    <div class="placeholder"></div>
                    <input class="button" type="button" name="" value="abort" v-on:click="close">
                    <input class="button" type="submit" v-bind:value="get_active()" v-on:click="submit">
                </div>
            </form>
        </div>
    </div>
  </div>
</template>
<script type="text/javascript">
const axios = require('axios')

    import list from './list.vue'
    import checkbox from './checkbox.vue'
    import license from './license.vue'
    import agb_text from '!vue-html-loader!../assets/agb.html'
    import lvb_text from '!vue-html-loader!../assets/lizensvereinbarungen.html'
    import { BASE_URL } from '../variable.js'

    export default{
        name:'loginpage',

        props: ['open_at_start', 'hide_register'],
        components:{
            list,
            checkbox,
            license
        },
        methods:{
            get_active(){return this.items[0].active? 'login': 'register'},
            submit(e){
                e.preventDefault();

                if(this.items[0].active){
                  this.$emit('login', {email: this.email, password: this.password});
/*                  axios({
                    method: 'post',
                    url: '/login',
                    data: {
                      email: this.email,
                      password: this.password
                    }
                  }).then(response => console.log(response));
*/
                }else{
                  if(this.password != this.password_again){
                    alert('passwords are not even!!!')
                    return;
                  }

                  axios({
                    method: 'post',
                    url: BASE_URL + '/register',
                    data: {
                      email: this.email,
                      password: this.password
                    }
                  }).then(response => console.log(response.data));
                }
            },
            open(selector){
              console.log(selector);

              this.items[0].active = (selector == 0);
              this.items[1].active = (selector == 1);

              this.visible = true;
            },
            close(){
              this.visible = false;
            }
        },
        data(){
            return{
                visible: false,
                items:[
                    {id: 0, text:'Login', active:true},
                    {id: 1, text: 'Register', active:false, click:()=>{
                      this.items[1].active = false;
                      this.items[0].active = true;
                    }}
                ],
                name: '',
                lastname: '',
                email: '',
                password: '',
                password_again: '',
                remain_signed_in: false,

                agb_text,
                lvb_text
            }
        },
        created(){
          axios.defaults.baseURL = BASE_URL;

        }
    }
</script>
<style media="screen" scoped>
#main_div{
  flex: 0 0 auto;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    /*margin-top: 60px;*/
    font-size: 20pt;
}
.toLogin{
  text-align: right;
  margin-bottom: 5px;

}

.opener{
  margin-left: 20pt;
}
*{
  font-size: 20pt;
}
.background{
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(0,0,0,0.8);
  display: block;
  z-index: 10;
}
.background > div{
  margin: 7.5%;
  background-color: white;
  padding: 20pt;
}
.hide{
  display: none!important;
}
form{
  display: flex;
  flex-direction: column;
}
.wrapper{
  flex: 0 0 auto;

  display: flex;
  flex-direction: row;
}
.wrapper label{
  flex: 1 0 auto;
}
.wrapper label:first-child{
  margin-right: 20pt;
}
label{
  flex: 0 0 auto;

  display: flex;
  flex-direction: column;
}
label.checkbox{
  flex-direction: row;
  margin-top: 20pt;
}
p{
  text-align: left;
  margin-bottom: 0;
}
input[type='checkbox']{
  height: 20pt;
  transform: scale(1.5);
  margin: auto 10pt;
}
.wrapper .button{
  margin-top: 20pt;
  flex: 1 0 auto;
  margin-left: 20pt;
  padding: 0 35pt;
}
.placeholder{
  flex: 0 1 100%;
}
</style>
