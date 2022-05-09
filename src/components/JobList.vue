<template>
   <div class="job-list">
       <p>Order by {{order}}</p>
       <transition-group name="list" tag="ul">
           <li v-for="job in orderedJobs" :key="job.id" >
               <h3>{{ job.title }} in {{job.location}} </h3>
               <div class="salary">
                   <p>{{job.salary}} rupees</p>
               </div>
               <div class="description">
                   <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Facilis ipsum, distinctio autem rerum id minima quis et, voluptas dignissimos fuga ad harum voluptatum maxime aut eos omnis illo odio architecto.</p>
               </div>
            </li>
       </transition-group>
   </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm'

export default defineComponent({
    props:{
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        order: {
            required: true,
            type: String as PropType<OrderTerm>
        }
    },
    setup(props){
        const orderedJobs = computed(() => {
            // using spread operator for the jobs array so as not to mutate the prop directly
            return [...props.jobs].sort((a:Job, b:Job) => {
                return a[props.order] > b[props.order] ? 1 : -1
            })
        })
        return {orderedJobs}
    }
   
})
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
   
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
     box-shadow: 0px 1px 4px 0px rgb(105 105 105 / 32%);
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
    .job-list p {
   font-weight: 700;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
      transition: all 1s;
  }

</style>
