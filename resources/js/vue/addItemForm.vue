<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon 
           icon="plus-square" 
           @click="addItem()"
           :class="[ item.name? 'active': 'inactive', 'plus' ]" />
    </div>
</template>
<script>
export default{
    data: function () {
            return { 
                item: {
                         name: ""
                      }
              }
    },
    methods: {
        addItem () {
               let name = (this.item.name);
            if( this.item.name = ""){
               return;
            }
            axios.post("api/item/store" , { 'item':{ 'name': name } })
            .then( res => {
               if( res.status == 201){
                  this.item.name == ""
                  this.$emit('reloadList');
               }
            })
            .catch( err => {
                console.log( err )
            });
             
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
   input {
      border: 0px;
      background: #C4DDFF;
      outline: none;
      padding: 7px;
      margin-right: 5px;
      width: 100%;
   }
   .plus {
      font: bold 25px Arial;
    }  
   .active {
      color: #3EC70B;
    }   
    .inactive {
     color: #001D6E;
    }
</style>

