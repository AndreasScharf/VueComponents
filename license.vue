<template>
    <div class="license_opener">
        <checkbox class="font-20pt" v-on:change="accept_change" v-bind:value="accept"/>
        <p>{{ this.pre_text }} <a v-on:click="open"> {{this.open_text}}</a> {{this.post_text}}</p>

        <div class="license-viewer" v-bind:class="{'hide':!this.viewer_open}">
            <div class="">
                <p>{{this.open_text}}</p>
                <div class="license-text" v-html="this.license_text">

                </div>
                <div class="wrapper">
                  <input class="button" type="button" v-on:click="accept_not" value="stimme nicht zu">
                  <input class="button" type="button" v-on:click="accept_it" value="stimme zu">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import checkbox from './checkbox.vue'
    export default{
        name: 'license',
        components:{
            checkbox
        },
        props: ['pre_text', 'open_text', 'post_text', 'license_text'],
        methods:{
            open(){
                this.viewer_open = true;
            },
            close(){
                this.viewer_open = false;
            },
            accept_change(value){
                this.accept = value;
                this.$emit('input', this.accept);
            },
            accept_it(){
                this.accept_change(true)
                this.close();
            },
            accept_not(){
                this.accept_change(false)
                this.close();
            }
        },
        data(){
            return{
                accept: false,
                viewer_open: false
            }
        },
        created(){
        }
    }
</script>
<style media="screen" scoped>
  .license-text{
    overflow-y: scroll;
    flex: 1 0 1;
    height: auto;
  }
  .license_opener{
    display: flex;
    flex-direction: row;
  }
  .license_opener p{
    flex: 1 0 auto;
    text-align: left;
  }
  .checkbox1{
    flex: 0 0 auto;
  }
  .license_opener p a{
    color: blue;
    text-decoration: underline;
    cursor: pointer
  }
  .license-viewer{
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    background-color: rgba(0,0,0,0.8);
    z-index: 11;
  }
  .license-viewer > div{
    background-color: white;
    margin: 7.5% 10%;
    padding: 10pt;
    height: calc(70% - 20pt);
    display: flex;
    flex-direction: column;
    position: relative;
  }
  .license-viewer div p{
    margin-top: 0;
    flex: 0 0 auto;
  }
  .wrapper{
    flex: 0 0 auto;
  }
  .hide{
    display: none!important;
  }
</style>
