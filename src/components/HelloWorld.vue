<script>
import axios from 'axios';

  export default{
    name:'helloworld',
    mounted(){
      axios.get('http://127.0.0.1:8000/api/v1/project-index')
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      })
    }
  }

</script>

<template>

<h2>ciao 2</h2>
</template>

<style scoped>

</style>
