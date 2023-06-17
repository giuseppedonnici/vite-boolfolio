<script>
import axios from "axios";

export default {
    name: 'SingleProjectPage',
    data() {
        return {
        baseUrl: "http://localhost:8000",
        project: null
        }
    },
    mounted() {
        const slug = this.$route.params.slug;
        axios.get(`${this.baseUrl}/api/projects/${slug}`).then(resp=> {
            this.project = resp.data.result;
        })
    }
}
</script>

<template>
  <div class="container">
    <div class="project-details" v-if="project">
        <h2>{{ project.title }}</h2>
        <p>{{ project.description }}</p>
    </div>
  </div>
</template>
