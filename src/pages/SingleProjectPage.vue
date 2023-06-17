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
        <h6>Tipologia: {{ project.type ? project.type.name : "Nessuna tipologia assegnata" }}</h6>
        <p v-if="project.technology > 0">
            <span class="me-2" v-for="technology in project.technologies">{{ technology.name }}</span>
        </p>
        <p v-else>{{ "Nessuna tecnologia assegnata" }}</p>
        <p>{{ project.description }}</p>
    </div>
  </div>
</template>
