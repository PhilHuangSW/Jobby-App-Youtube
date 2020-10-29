<template>
  <b-container>
    <b-row align-v="center">
      <job-card v-for="job in jobs" :key="job.id" :name="job.name"></job-card>
    </b-row>
    <b-pagination
      v-model="currentPage"
      :total-rows="rows"
      :per-page="perPage"
      first-text="First"
      prev-text="Prev"
      next-text="Next"
      last-text="Last"
      >
    </b-pagination>
  </b-container>
</template>

<script>
// @ is an alias to /src
import JobCard from '@/components/JobCard.vue'

export default {
  name: "Home",
  components: {
    'job-card' : JobCard
  },
  mounted(){
    this.fetchData();
  },
  data(){
    return {
      jobs: [],
      currentPage: 1,
      rows: 1,
      perPage: 3
    }
  },
  methods: {
    async fetchData(){
      const res = await fetch("jobs.json");
      const val = await res.json();
      this.jobs = val;
      this.rows = this.jobs.length;
      console.log(val);
    }
  }
};
</script>
