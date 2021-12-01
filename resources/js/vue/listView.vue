<template>
    <div>
        <div v-for="item in items" :key="item.id" >
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
        },
        mounted() {
            console.log('from created list view',this.items);
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
