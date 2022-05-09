<template>
 
  <!-- <button class="action_button" @click="changeName('Zenith Amber')" >Change Name</button> -->
 
    <header>
       <h1>Job Listing App</h1>
      <p>Sort jobs with provided option</p>
      <div class="order">
        <button @click="handleClick('title')" > Order by title </button>
        <button @click="handleClick('salary')" > Order by salary </button>
        <button @click="handleClick('location')" > Order by location </button>
      </div>
    </header>


 
  <JobList :jobs='jobs' :order='order' />
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRef, toRefs } from 'vue';
import JobList from './components/JobList.vue'
import Job from  "./types/Job"
import OrderTerm from '@/types/OrderTerm'

export default defineComponent({
  name: 'App',
  components: { JobList },
  setup(){

    // using reactive component
    // const state = reactive({
    //   name: "Sanmi Salami",
    //   age: "34" as number | string
    // })
    // return { ...toRefs(state) }

    // using refs
    // const name = ref("Shaun Lord")
    // const age = ref<number | string>(90)

    // return {name, age}

    const jobs = ref<Job[]>([
      {title: "Farm Worker", salary: 100000, location: 'Lagos, Nigeria', id:1 },
      {title: "Bassist", salary: 705000, location: 'Maiduguri, Nigeria', id:2 },
      {title: "Pharmacist Worker", salary: 900000, location: 'Kaduna, Nigeria', id:3 },
      {title: "Actor", salary: 200000, location: 'Nairobi, Kenya', id:4 },
      {title: "Playboy", salary: 1100000, location: 'Osun, Nigeria', id:5 }
    ])

    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return {jobs, handleClick, order }

  },
  // data(){
  //   return {
  //     name:"Sanmi Micheals",
  //     age: 45
  //   }
  // },


  methods:{
    // changeName(name:string){
    //   this.name = name
    // }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  header h1{
    margin-bottom: 0;
  }
   header p{
    margin: 4px 12px;
    
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>
