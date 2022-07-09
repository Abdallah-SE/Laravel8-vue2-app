<template>

    <div class="item">
        <input 
            type="checkbox" 
            @change="updateCheck()" 
            v-model="item.completed"
       />
       <span :class="[item.completed ? 'completed' : '', ' itemtext' ]" > {{ item.name }} </span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>
<script>
export default{
   props: ['item'],
   methods: {
      updateCheck() {
         axios.put('api/item/' + this.item.id , {
          item: this.item
         })
         .then( res => {
            if( res.status == 200 ){
               this.$emit('changed');
            }
         })
         .catch( err => {
            console.log( err );
         });
      },
    removeItem(){
       axios.delete('api/item/' + this.item.id)
       .then( res => {
          if( res.status == 200){
             this.$emit('changed');
          }
       })
       .catch( err => {
          console.log( err );
       });
    }
   }
}
</script>

<style scoped>
.item {
   display: flex;
   justify-content: center ;
   align-items: center;
   padding: 25px;
}
.completed {
   text-decoration: line-through;
   color: red;
   
}
.itemtext {
   width: 100%;
   margin-left: 2px;
   font: bold 25px Arial;
}

.trashcan {
    background: #e6e6e6;
    color: red;
    outline: none;
    border: none;
    font: bold  25px Arial;
    border: 2px solid blue;

}
</style>


