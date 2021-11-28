<template>
    <div class="addItem">
        <input type="text" v-model="item.name"/>
        <font-awesome-icon
            @click="addItem()"
            icon="plus-square"
            :class="[item.name? 'active':'inactive','plus']"
        />
    </div>
</template>

<script>
    export default {
        data:function () {
            return {
                item:{
                    name:""
                }
            }
        },
        methods:{
            addItem(){
                if(this.item.name===''){
                    return;
                }
                axios.post('/api/item/store',{
                    item:this.item
                })
                .then(response=>{
                    if(response.status==201){
                        this.item.name='';
                        this.$emit('reloadList')
                    }
                })
                .catch(error=>{
                    console.log(error)
                })
            }
        }
    }
</script>
<style scoped>
    .addItem{
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input{
        background: #f7f7f7;
        margin-right:5px ;
        padding: 10px;
        outline: none;
        border: 0px;

    }
    .active{
        color:#00CE25;
    }
    .plus{
        font-size: 20px;
    }
    .inactive{
        color:#999999
    }
</style>
