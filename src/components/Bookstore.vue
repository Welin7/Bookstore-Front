<template>
   <div>
    <h1>{{ msg }}</h1>    
    <table border="black">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Price</th>
          <th>Category</th>
          <th>Author</th>  
        </tr>
      </thead>
       <tbody>
         <tr v-for="book in bookstores" v-bind:key="book.id">
           <td>{{ book.id }}</td>
           <td>{{ book.name }}</td>
           <td>{{ book.price }}</td>
           <td>{{ book.category }}</td>
           <td>{{ book.author }}</td>  
         </tr>
       </tbody>     
    </table>
   </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Bookstore',
  props: {
    msg: String
  },

  data: () => {
    return {
      bookstores: [],
    }
  },

  //metod that return  the request of data
  methods: {
    list: (scope) => {
      axios.get(`https://localhost:44371/Books`).then((response)=> {
        console.log(response);
        scope.bookstores = response.data;
      })
    }
  },

  //metod created pass the scope to axios execute the call
  created() {
    this.list(this);
  }
}
</script>


