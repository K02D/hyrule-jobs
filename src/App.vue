<template>
  <div class="app">
    <header>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobsList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from './types/Job';
import OrderBy from './types/OrderBy';
import JobsList from './components/JobsList.vue';

export default defineComponent({
  name: 'App',
  components: { JobsList },
  setup() {
  
  const jobs = ref<Job[]>([ // use ref() to make jobs array 'reactive'
    { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
    { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
    { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
    { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4' },
    { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' }
  ])

  const order = ref<OrderBy>('title'); // can only be one of 3 values specified by the OrderBy tpye

  const handleClick = (orderSelected: OrderBy) => {
    order.value = orderSelected;
    // sort based on the order selected
  }
  return { // everything that we return can be used the template above
    jobs,
    handleClick,
    order
  }
}
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
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
