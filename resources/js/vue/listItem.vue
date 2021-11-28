<template>
    <div class="item">
        <input
            type="checkbox"
             @change="upateCheck()"
            v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed':'','itemText']">{{item.name}}</span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
    export default {
        props:['item'],
        methods:{
            upateCheck(){
                axios.put('api/item/'+this.item.id,{
                    item:this.item
                })
                .then(response=>{
                    if(response.status==200){
                        this.$emit('itemchanged')
                    }
                })
                .catch(error=>{
                    console.log(error);
                })
            },
            removeItem(){
                axios.delete('api/item'+this.item.id)
                .then(response=>{
                    if(response.status==200){
                        this.$emit('itemchanged')
                    }
                })
                .catch(error=>{
                    console.log(error);
                })
            }
        },
        created() {
            console.log(this.item)
        }
    }
</script>

<style scoped>
    .completed{
        text-decoration: line-through;
        color:#999999;
    }
    .itemText{
        width: 100%;
        margin-left: 20px;
    }
    .item{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .trashcan{
        background: #6E6E6E;
        border: none;
        color:#ff413c;
        outline: none;
    }
</style>
