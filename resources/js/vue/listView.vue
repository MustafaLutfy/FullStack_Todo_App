<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <ListItem 
                :item="item"
                class="item"
                v-on:itemchanged="$emit('reloadlist')"
            />
        </div>
    </div>
</template>
<script>
import ListItem from './listItem.vue';
    export default{
    props: ["items"],
    components: { ListItem },
}
</script>
<style scoped>
    .item{
        background-color: #e6e6e6;
        padding: 10px;
        margin-top: 5px;
    }
</style>