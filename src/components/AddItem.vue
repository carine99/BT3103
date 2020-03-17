<template>
  <div id=app>
    <h1>Add Item Page</h1>
    <form id="fm1">
        <label>Item Name</label>
        <input type="text" v-model.lazy="item.name" required/>
        <label>Item Category</label>
        <input type="text" v-model.lazy="item.category"/>
        <label>Time Ordered</label>
        <input type="time" v-model="item.time"/>
        <label>Delivery Mode</label>
        <select v-model="item.delivery">
          <option disabled value="">Please select one</option>
          <option>Free Delivery</option>
          <option>Fast Delivery</option>
          <option>Self-Collection</option>
        </select>
        <button v-on:click.prevent="addItem">Add Item</button>
        
    </form>
  </div>
</template>

<script>

import database from '../firebase.js'
export default {

  data(){
    return{
        msg:"Add Item",
        item:{
          name:'',
          category:'',
          time: '',
          delivery: ''
        },
        
        
        }
  },
  methods:{
    addItem:  function () {
          //Save item to database
          //database.collection('items').doc().set(this.item);
          database.collection('items').add(this.item);
          this.item.name="";
          this.item.category="";
          this.item.time="";
          this.item.delivery="";
          alert("I am in the DB .... :-) Item saved successfully")
          
        }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#app *{
    box-sizing: border-box;
}
#app{
    margin: 20px auto;
    max-width: 500px;
}

p{
    align-content: center;
    color:ivory;
}
label{
    display: inline-block;
    margin: 20px 0 10px;
    width:50%;
    align-content:left;

}
input[type="text"], input[type="time"], select{
    display: inline-block;
    padding: 8px;
    width:50%;
}
</style>