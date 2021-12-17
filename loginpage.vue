<template>
  <div id="main_div">
    <div class="toLogin" v-bind:class="{'hide':this.open_at_start}">
      <input type="button" value="Sign In" v-on:click="open(0)" class="opener button">
      <input type="button" value="Sign Up" v-on:click="open(1)" class="opener button">
    </div>
    <div class="user" v-bind:class="{'hide':true}">

    </div>
    <div class="loginpage background" v-bind:class="{'hide':!(this.visible || this.open_at_start)}">
        <div class="" style="display: flex; flex-direction: column;">
            <div v-if="$isMobile()" class="logo icon" :style="`flex: 0 0 70pt; background-image var(--logo); margin: 0 20pt;`"></div>
            <list class="navbar" v-bind:items="items"/>
            <form>
                <!--Login item 0 Register item 1-->
                <div class="wrapper" v-bind:class="{'hide': !items[1]}">
                  <md-field class="">
                    <label>Vorname</label>
                    <md-input v-model="name"></md-input>
                  </md-field> 
                  <md-field class="">
                    <label>Nachname</label>
                    <md-input v-model="lastname"></md-input>
                  </md-field>
                </div>


                <md-field class="">
                  <label>email/username</label>
                  <md-input v-model="email"></md-input>
                </md-field>
                <md-field>
                  <label>password</label>
                  <md-input type="password" v-model="password"></md-input>
                </md-field>
                <md-switch v-model="remain_signed_in" class="md-primary" :class="{'hide': !items[0].active}">remain signed in</md-switch>

                <md-field :class="{'hide': items[1] ? !items[1].active:true}">
                  <label>password repeat</label>
                  <md-input type="password" v-model="password_again"></md-input>
                </md-field>


                <license v-bind:class="{'hide': items[1]? !items[1].active: true}" pre_text="Ich stimme den " open_text="Lizensvereinbarungen" post_text=" zu" v-bind:license_text="lvb_text"/>
                <license v-bind:class="{'hide': items[1]? !items[1].active: true}" pre_text="Ich stimme den " open_text="AGBs" post_text=" zu" v-bind:license_text="agb_text"/>
                <div class="wrapper btn">
                    <div class="placeholder"></div>
                    <md-button class="button login md-primary" :class="{'hide':!items[1]}" type="button" name="" value="abort" v-on:click="close">abort</md-button>
                    <md-button class="button login  md-primary" type="submit" v-bind:value="get_active()" v-on:click="submit">login</md-button>
                </div>
            </form>
        </div>
    </div>
  </div>
</template>
<script type="text/javascript">

    import list from './list.vue'
    import license from './license.vue'
    import agb_text from '!vue-html-loader!@/assets/agb.html'
    import lvb_text from '!vue-html-loader!@/assets/lizensvereinbarungen.html'

    export default{
        name:'loginpage',

        props: ['open_at_start', 'hide_register'],
        components:{
            list,
            license
        },
        methods:{
            get_active(){return this.items[0].active? 'login': 'register'},
            submit(e){
                e.preventDefault();

                if(this.items[0].active){
                  this.$emit('login', {email: this.email, password: this.password});

                }else{
                  if(this.password != this.password_again){
                    alert('passwords are not even!!!')
                    return;
                  }
 }
            },
            open(selector){

              this.items[0].active = (selector == 0);
              if(this.items[1])
                this.items[1].active = (selector == 1);

              this.visible = true;
            },
            close(){
              this.visible = false;
            }
        },
        data(){
            const items = [{id: 0, text:'Login', active:true}]
            if(!this.$props.hide_register)
              items.push({id: 1, text: 'Register', active:false, click:()=>{
                      //this.items[1].active = false;
                      //this.items[0].active = true;
                    }})
            return{
                visible: false,
                items:items,
                name: '',
                lastname: '',
                email: '',
                password: '',
                password_again: '',
                remain_signed_in: 0,

                agb_text,
                lvb_text
            }
        },
        created(){

        },
        mounted(){
          
        }
    }
</script>
<style media="screen" >
#main_div{
  flex: 0 0 auto;
}

.toLogin{
  text-align: right;
  margin-bottom: 5px;

}

.opener{
  margin-left: 20pt;
}


.loginpage.background{
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(0,0,0,0.8);
  display: block;
  z-index: 10;
}
.loginpage.background > div{
  margin: 7.5%;
  background-color: white;
  padding: 20pt;
}
.loginpage .hide{
  display: none!important;
}
.loginpage form{
  display: flex;
  flex-direction: column;
}
.loginpage .wrapper{
  flex: 0 0 auto;

  display: flex;
  flex-direction: row;
}
.loginpage .wrapper label{
  flex: 1 0 auto;
}
.loginpage .wrapper label:first-child{
  margin-right: 20pt;
}
.loginpage label{
  flex: 0 0 auto;

  display: flex;
  flex-direction: column;
}
.loginpage label.checkbox{
  flex-direction: row;
  margin-top: 20pt;
}
.loginpage p{
  text-align: left;
  margin-bottom: 0;
}
.loginpage input[type='checkbox']{
  height: 20pt;
  transform: scale(1.5);
  margin: auto 10pt;
}
.loginpage .wrapper .button{
  margin-top: 20pt;
  flex: 1 0 auto;
  margin-left: 20pt;
  padding: 0 35pt;
}
.loginpage .placeholder{
  flex: 0 1 100%;
}
@media screen and (max-device-width: 800px) {/*für mobil*/

  .loginpage.background{
    display: flex;
    width: 100vw;
  }
  .loginpage.background > div{
    flex: 1 0 0;
    margin: 0;
    padding: 0pt;
    
  }
  .loginpage ul{
    margin: 0 20pt;
    margin-top: 15%;
  }
  .loginpage form{
    margin: 0 20pt;
  }
  .loginpage div.wrapper.btn{
    flex-direction: column-reverse;
  }
  .loginpage div.wrapper.btn input.button{
    margin-left: 0;
    margin: 5pt 0;
  }
  .loginpage label.checkbox .wrapper.font-20pt div.checkbox{
    margin: auto 5pt
  }
}
</style>
