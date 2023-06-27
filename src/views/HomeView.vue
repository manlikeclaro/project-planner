<template>
  <div class="home">
    <FilterNav @filter="current = $event" :current="current"/>
    <div v-if="projects.length">
      <div v-for="project in filteredproject" :key="project.id">
        <SingleProject :project="project" @delete="handledelete" @complete="handlecomplete"/>
      </div>
    </div>
    
    <!-- <div>
      <div v-for="project in projects" :key="project.id">
        <trialVue :project="project" @filter="filte = project.postId"/>
        
      </div>
    </div> -->
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '@/components/FilterNav.vue'
import trialVue from '@/components/trial.vue'

export default {
  name: 'HomeView',

  data(){
    return {
      projects: [],
      current: 'all',
      url: "http://localhost:3000/projects",
      filte: ''
    }
  },

  components: { SingleProject, FilterNav, trialVue},

  mounted(){
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => this.projects = data)
      .catch(err => console.log(err.message))
      console.log('mounted')

    // fetch('https://jsonplaceholder.typicode.com/comments')
    //   .then(res => res.json())
    //   .then(data => this.projects = data)
    //   .catch(err => err.message)
  },

  updated(){
    this.checkfilte()
  },

  methods: {
    handledelete(id){
      this.projects = this.projects.filter((project) => { return project.id !== id })
    },

    handlecomplete(id){
      let p = this.projects.find((project) => { return project.id === id })
      p.complete = !p.complete
    },

    checkfilte(){
      console.log(this.filte)
    }
  },

  computed: {
    filteredproject(){
      if (this.current === 'complete'){
        return this.projects.filter(project => project.complete)
      } 
      if (this.current === 'ongoing'){
        return this.projects.filter((project) => !project.complete)
      }
      return this.projects
    },

    filteredcomments(){
      if(this.filte === ''){
        return this.projects.filter(project => project.postId === 1)
      }
    }
  }
}
</script>

<style>
  
</style>