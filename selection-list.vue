<template>
    <div class="vertical-wrapper"> 
        <div v-if="topSelectionAll" class="list-item horizontal-wrapper" style="border-bottom: solid 1pt #2c3e50; flex: 0 0 auto;">
            <md-field v-if="searchBar" style="flex: 0 0 auto; flex: 0 0 0; margin: 5pt 0;">
                <label>Suchen</label>
                <md-input v-model="searchText" ></md-input>
            </md-field>

            <div class="placeholder"></div>
            <md-switch class="md-primary" @change="e => list.forEach(i => i.active = e)" v-model="forAllItems"></md-switch>
        </div>
        <div style="overflow-y:scroll; flex: 1 0 0;">
            <div v-for="item in list.filter(e => ((e.name)? e.name.includes(searchText):false) || ((e.text)? e.text.includes(searchText): false))" 
                :key="item.key" 
                class="list-item horizontal-wrapper">
                <span style="margin: auto 5pt; flex: 0 0 auto;">{{item.name || item.text}}</span>
                <div class="placeholder"></div>
                <md-switch class="md-primary" @change="$emit('item-selection-change', list)"  v-model="item.active"></md-switch>
            </div>
        </div>
    </div>
</template>
<script>
import { v4 as uuidv4 } from 'uuid';

export default {
    name:'selection-list',
    props: {'items':Array, 'top-selection-all':Boolean, 'search-bar':Boolean},
    watch: { 
        'items': function(items) { 
          items.forEach(e => {e.key = uuidv4() })
          this.list = items
        }
    },
    methods: {
        uuidv4:uuidv4,
    },
    data(){
        this.$props.items.forEach(e => {e.key = uuidv4() })
        
        return{
            list: this.$props.items,
            forAllItems: false,
            searchText: ''
        }
    }
}
</script>
<style>
.list-item .md-switch.md-primary.md-theme-default{
    flex:  0 0 auto;
}
</style>