<script>
import axios from 'axios';

  export default{
    name:'ProjectCard',
    data(){
      return {
          projects :[],
          links: []
        }


    
},
    methods:{
          movePage(target){
            axios.get(target)
            .then(response => {
              const data = response.data;

              this.projects = data.projects.data;
              this.links = data.projects.links;
              
            })
              .catch(error => {
          console.log(error);
        });
    }
  },
    
    mounted(){
      axios.get('http://127.0.0.1:8000/api/v1/project-index')
      .then(response => {
        const data = response.data;
        console.log(response.data);

        this.projects = data.projects.data;
        this.links = data.projects.links;


      })
      
      .catch(error => {
        console.log(error);
      })
    }
  }

</script>

<template>
  <div class="container">
    <h2>
      PROJECTS
    </h2>
    <ul>
      <li v-for="project in projects" :key="project.id">
        {{ project.name }}
      </li>
    </ul>
  </div>
  <div class="pages mt-3">
      <div v-for="(link, index) in links"
      key="index"
      class="page mx-1 btn"
      :class="(link.active ? 'btn-warning' : 'btn-secondary' )
        + (link.url == null ? 'd-none text-light' : '')"
    
      v-html="link.label"
      @click="movePage(link.url)"
      >
    
      </div>
    </div>
</template>

<style scoped>

ul{
    list-style: none;
    
  }
</style>
