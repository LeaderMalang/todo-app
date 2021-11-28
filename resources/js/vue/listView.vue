<template>
    <div>
        <div v-for="{item,index} in items" :key="index" >
            <list-item
            :item="item"
            class="item"
            v-on:itemchanged="$emit('reloadList')"
            />
        </div>
    </div>
</template>

<script>
    import listItem from "./listItem";
    export default {
        props:['items'],
        components:{
            listItem
        }
    }
</script>
<style scoped>
    .item{
        background: #6E6E6E;
        padding: 5px;
        margin-top: 5px;
    }
</style>
