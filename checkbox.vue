<template>
    <div class="wrapper" v-bind:value="this.clicked" v-on:click="item_clicked">
        <div class="checkbox" v-bind:class="{'clicked':this.clicked}">

        </div>
        <p v-bind:class="{'hide':this.text == ''}">
            {{ text }}
        </p>
    </div>
</template>
<script type="text/javascript">
export default{
    name:'checkbox',
    props: {
        text:{
            type: String
        },
        value:{
            type: Boolean
        }
    },
    methods:{
        item_clicked(){
            this.clicked = !this.clicked;
            this.$emit('input', this.clicked);
        /*    this.$emit('change', this.clicked);
        */}
    },
    data(){
        return{
            clicked: false
        }
    },
    created(){
        this.clicked = this.$props.value;
    },
    watch: {
        value: {
            immediate: true,
            handler () {
                this.clicked = this.$props.value;
            }
        }
    }
}
</script>
<style media="screen" scoped>
    .wrapper{
        display: flex;
        flex-direction: row;
    }
    .wrapper p{
        flex: 1 0 auto;
        text-align: left;
    }
    div.checkbox{
        margin: auto 20pt;
        flex: 0 0 60pt;
        height: 34pt;
        width: 68pt;
        border-radius: 19pt;
        padding: 4pt;
        background-color: lightgrey;
        transition: background-color 0.4s
    }
    div.checkbox:before{
        content: '';
        display: block;
        width: 34pt;
        height: 34pt;
        top: 0;
        left: 0;
        background-color: white;
        border-radius: 17pt;
        transition: margin 0.4s;
    }
    div.checkbox.clicked{
        background-color: #42b983;;
    }
    div.checkbox.clicked:before{
        margin-left: calc(50% - 4pt);
    }
    .font-20pt .checkbox{
        height: 24pt;
        flex: 0 0 40pt;
        width: 48pt;
        border-radius: 15pt;
        padding: 3pt;

    }
    .font-20pt .checkbox:before{
        width: 24pt;
        height: 24pt;
        border-radius: 12pt;
    }
    .font-20pt .checkbox.clicked:before{
        margin-left: calc(50% - 3pt);
    }
    .hide{
        display: none;
    }
</style>
