<template>
    <div class="addItem">
        <input type="text" placeholder="Add task" v-model='item.name' />
        <font-awesome-icon 
        icon="fa-solid fa-square-plus" 
        @click="addItem"
        
        :class="[item.name ? 'active' : 'inactive']"
        />
    </div>
</template>
<script>
import axios from 'axios';

    export default{
        data: function(){
            return {
                item: {
                    name: '',
                }
            }
        },
        methods:{
            addItem(){
                if (this.item.name == ''){
                    return;
                }
                axios.post('api/item/store',{
                    item: this.item,
                })
                .then(response => {
                    if(response.status == 201){
                        this.$emit('reloadlist');
                        this.item.name = '';
                    }
                })
                .catch(error => {
                    console.log('error');
                })
            }
        }
    }
</script>
<style scoped>
    .addItem{
        display: flex;
        align-items: center;
        justify-content: center;

    }
    .fa-square-plus{
        color: rgba(0, 0, 0, 0.76);
        font-size: 35px;
        margin-left: 10px;
        cursor: not-allowed;
    }
    
    input{
        border-radius: 20px ;
        outline: none;
        border: none;
        width: 80%;
        font-size: 18px;
        color: #fff;
        padding: 8px;
        background-color: rgba(0, 0, 0, 0.801);
    }
    .active{
        color: rgba(0, 0, 0, 0.76);
        cursor: pointer;
    }
    .active:hover{
        color: rgba(0, 0, 0, 0.884);
    }
    .inactive{
        color: rgba(0, 0, 0, 0.397);
    }
</style>