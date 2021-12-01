<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item-form

                v-on:reloadList="getlist()"
            ></add-item-form>
        </div>
        <list-view :items="items"
        v-on:reloadList="getlist()"
        />
    </div>
</template>
<script>
    import addItemForm  from "./addItemForm";
    import listView from "./listView";
    export default {
        components:{
            addItemForm,
            listView
        },
        data:function () {
            return {
                items:[]
            }
        },
        methods:{
            getlist(){
                axios.get('api/items')
                .then(response=>{
                    this.items=response.data;
                    console.log('from methods App',this.items)
                })
                .catch(error=>{
                    console.log(error)
                })


            }
        },
        created() {
            this.getlist();
            console.log('from created App',this.items);
        }
    }
</script>
<style scoped>
    .todoListContainer{
        width: 350px;
        margin: auto;
    }
    .heading{
        background: #6E6E6E;
        padding: 10px;
    }
    #title{
        text-align: center;
    }
</style>
