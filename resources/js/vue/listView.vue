<template>

    <div>
        <div v-for="item in items" :key="item.id">           
        <list-item
               :item="item"
               class="item"
               v-on:changed="$emit('reloadList')"
        />
        </div>
    </div>
</template>
<script>

import listItem from './listItem';

export default{
   props: ['items'],
   components: {
      listItem
   }
   
}
</script>

<style scoped>
.item {
    background: #e6e6e6;
    padding: 5px;
    margin-top: 9px;
}
</style>

