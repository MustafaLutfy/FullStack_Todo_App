<template>
    <div class="item">
        <input 
        type="checkbox" 
        @change="updateCheck()"
        v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed': '', 'itemText']">{{item.name}}</span>
         <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash"></font-awesome-icon>
         </button>
    </div>
</template>
<script>
import axios from 'axios';

    export default{
        props: ['item'],
        data: function(){
            return{
                comp: 1,
            }
        },
        methods: {
            updateCheck() {
                axios.put('api/item/' + this.item.id, {
                    item: this.item
                }).then(response => {
                    if (response.status == 200){
                        this.$emit('itemchanged');
                    }
                }).catch(error => {
                    console.log(error)
                })
            },
            removeItem() {
                axios.delete('api/item/' + this.item.id, )
                .then(response => {
                    if (response.status == 200){
                        this.$emit('itemchanged');
                    }
                }).catch(error => {
                    console.log(error)
                })
            }
        }
    }
</script>
<style scoped>
    .completed{
        text-decoration: line-through;
        color: #999999;
    }
    .itemText{
        width: 100%;
        margin-left: 20px;
    }
    .item {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .trashcan{
        background-color: transparent;
        padding: 8px 10px;
        border: none;
        outline: none;
        color: rgb(92, 92, 92);
        font-size: 20px;
        cursor: pointer;
        transition: 0.3s;
    }
    .trashcan:hover{
        color: rgb(41, 41, 41);
    }
</style>