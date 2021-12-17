<template>
    <div class="quote">
        <div class="text" v-html="'&quot;' + quote + '&quot;'">
        </div>
        <div class="person horizontal_wrapper">
            <div class="placeholder"></div>
            <div class="placeholder"></div>
            <div class="placeholder"></div>

             <div v-if="person.img" class="image">
                <div :style="`background-image:url('${person.img}')`"></div>
            </div>
            <div class="vertical_wrapper">
                <h2>{{person.name}}</h2>
                <h3>{{person.position}}</h3>
            </div>

        </div>
    </div>
</template>
<script>
export default {
    name:'quote',
    props:{
        quote: String,
        person: Object,
    }
}
</script>
<style>
.quote{
    margin: 25pt auto;
    font-family: 'Amiko';
    color: #4e4e4e;

}
.quote .text{
    margin: 20pt auto;
    line-height: 40pt;
    font-family: 'Amiko';
    font-size: 40pt;
}
.person{
    margin: 0 ;
}
.person h2{
    margin-bottom: 0;
    font-size: 24pt;
    line-height: 24pt;
    text-align: right;
}
.person h3{
    margin-top: 0;
    font-size: 20pt;
    line-height: 20pt;
    text-align: right;

}
.person .image{
    margin: 5pt 0;
    flex: 0 0 70pt;
    margin-right: 20pt;
}
.person .image div{ 
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;

}
</style>