<script>

</script>

<template>

    <div class="todoListComponents">
        <h1 class="appTitle">Laravel Vue Todo App</h1>
        <div class="heading">
           <h2 id="title"> Create One </h2>
           <add-item-form 
              v-on:reloadList="getList()"
           />
        </div>
        <list-view 
            :items="items"
            v-on:reloadList="getList()"
         />
    </div>
</template>
<script>

import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";

export default{
       components: { 
            addItemForm,
            listView
        },
        data: function (){
             return {items: []}
        },
        methods: {
            getList() {
                axios.get('api/items').then( res => {
                   this.items = res.data;
                }).catch( err => {
                   console.log(err);
                });
            }
        },
        created() {
           this.getList();
        }
    }
</script>

<style scoped>
    .todoListComponents {
        width : 500px;
        margin: auto;
        margin-top: 0px;
        padding-top: 0px;
        border-top: 3px solid #37E2D5;
    } 
    .appTitle {
        background : #C70A80;
        padding: 10px;
        text-align: center;
        color: white;
    } 
   .heading {
        background : #FBCB0A;
        padding: 10px;
    }   
   #title {
        text-align : center;
        margin: auto;

    }
</style>

