<template>
    <div class="todoContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <addItemForm/>
        </div>
        <ListView 
        :items="items"
        v-on:reloadlist="getList()"
        />
    </div>
</template>

<script>
    import addItemForm from './addItemForm.vue';
    import ListView from './listView.vue';

    export default {
    components: { ListView , addItemForm},
    data: function(){
            return {
                items: []
            }
        },
    methods: {
        getList(){
            axios.get('api/items')
            .then(response => {
                this.items = response.data
            })
            .catch(error => {
                console.log(error);
            })
        }
    },
    created(){
        this.getList();
    }
}
</script>
<style scoped>
    .todoContainer{
        width: 40vw;
        margin: auto;
    }
    .heading{
        background: #e6e6e6;
        padding: 10px;
    }
    #title {
        text-align: center;
    }
</style>