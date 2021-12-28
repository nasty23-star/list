<template>
<h1>Movie list</h1>


<form @submit.prevent>
 
    <div class="count"><span>to watch</span>
<span class="watch"> {{ items.length }} </span></div>

<label for="name">Name</label>
<input type="text" 
v-model="name"

/> 
    <label for="genre">Genre</label>
    <select v-model="genre">

      <option value="none">none</option>
            <option value="com">com</option>
            <option value="hor">hor</option>
            <option value="dr">dr</option>
        </select>
     <label for="about">About</label>
    <input type="text" v-model="about" placholder="write about">
    <label form="year">Year</label>
    <input  type="number" placeholder="year"
    v-model="year" />
  
  <button type="btn" @click="addMovie()">+</button>
</form>

<table class="table" v-if="items.length">
  <thead>
     <tr>
       
        <th >
          Name</th>
        <th >
          Genre
        </th>
        <th> About 

        </th>
        <th @click="sortHighest">
            Year <br>sort by year</th>
            <th>Delete</th>
     </tr>
  </thead>
    <tbody >
      <tr v-for="item,index in items"  :key="item.index" :item="item" 
    >
        
        <td>  {{ item.name }} </td>
        <td> {{ item.genre }} </td>
        <td> {{ item.about }} </td>
        <td> {{ item.year }} </td>
        <td><button class="delete" @click="deleteItem(index)">delete</button>  </td>
      </tr>
      
    </tbody>
    
</table>
<label>Filter by name</label>
  <input type="text" v-model="search" placeholder="search name..."/>
  <label>Filter by genre</label>
<input v-model="selected" placeholder="filter by genre"/>
 



        
</template>


<script>
import { computed } from '@vue/reactivity'



export default {
  name: 'App',
  data() {
    return {
      items: [],
      item: {},

item: { name: this.name, genre: this.genre, year: this.year, about: this.about, },    
     search: '',
 genre: '',
 
    }
  
   
     
  
 
  },
    
  computed: {
    items() {
     
      let filter = new RegExp(this.search, 'i')
      return this.items.filter(item => item.name.match(filter))
      
    }
  },
  methods: {
  
   addMovie() {
   
   if (this.name === "") {return};

     this.items.push({
     index: this.items.length,
       name: this.name,
       genre: this.genre,
       year: this.year,
       about: this.about,
       time: this.time
     })

    this.name = '';
    this.year = null
    },
  sortHighest() {
      this.items.sort((a, b) => a.item < b.item ? 1 : -1);
    },

deleteItem(index) {
    this.items.splice(index, 1)
    },
  }
}
 
  
  
   
    
  
  
</script>

<style>
*{
  background-color: lightgray;
}
h1 {
  padding-left: 20px;
  font-size: 30px;
  color: darkcyan;
}
.count {
  display: flex;
justify-content: space-between;
color: red;
}
span {
  width: 100%;
  background-color: teal;
  padding-left: 5%;
  
}
form {
  width: 300px;
  background-color: teal;
  margin-bottom: 30px;
  margin-left: 20px;
  margin-top: 30px;
}
.form {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
}
th {
  background-color: white;
}
label {
  width: 100%;
  background-color: rgb(49, 49, 109);
  display: flex;
  justify-content: center;
  color: white;
  font-size: 20px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

button {
  margin-top: 20px;
 width: 100%;
  border: white;
  background-color: rgb(49, 49, 109);
  color: white;
}
.del {
  width: 10%;
  background-color: white;
  margin: 0;
}

.delete  {
  padding-right: 20px;
  cursor: pointer;
  margin: 0;
  background-color: transparent;
  color: black;
  font-size: 30px;
  
  width: 100%;
  height: 20px;
  display: flex;
  text-align: center;
  align-items: center;
  justify-content: center;
  align-self: center;
}
::placeholder {
  padding-left: 20px;
}
table {
  width: 100%;
  background-color: lightblue;
  border: none;
  font-size: 15px;
  font-family:'Courier New', Courier, monospace;
}
td {
 background-color: lightseagreen;
 padding-left: 20px;
 color: black;
 width: 20%;
}
.btn {
  width: 100px;
  border-radius: 50%;
  margin: 20px;
}
</style>