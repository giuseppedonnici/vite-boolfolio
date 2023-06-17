<script>
import axios from "axios";
import ProjectCard from "../components/ProjectCard.vue";
import { store } from "../store";

export default {
  name: "ProjectsPage",
  data() {
    return {
      projects: [],
      currentPage: 1,
      lastPage: null,
      totalProject: 0,
      store,
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects(pageNumber = 1) {
      axios.get(`${this.store.apiBaseUrl}/api/projects`, {
        params: {
          page: pageNumber
        }
      }).then((resp) => {
        this.projects = resp.data.result.data;
        this.currentPage = resp.data.result.current_page;
        this.lastPage = resp.data.result.last_page;
        this.totalProject = resp.data.result.total;
      });
    },
  },
  components: { ProjectCard },
};
</script>

<template>
  <div class="container">
    <h2>Lista dei progetti</h2>
    <div class="text-end">Trovati {{ totalProject }} progetti</div>
    <div class="row row-cols-3 g-3">
      <div class="col" v-for="project in projects" :key="project.id">
        <ProjectCard :project="project" />
      </div>
    </div>
    <!-- Paginazione -->
    <nav v-if="lastPage" class="mt-4 d-flex justify-content-center" aria-label="Page navigation example">
      <ul class="pagination">
        <li class="page-item" :class="{'disabled' : currentPage === 1}"><a @click.prevent="getProjects(currentPage - 1)" class="page-link" href="#">Previous</a></li>
        <li class="page-item" :class="{'active' : pageNum === currentPage}" v-for="pageNum in lastPage"><a @click.prevent="getProjects(pageNum)" class="page-link" href="#">{{ pageNum }}</a></li>
        <li class="page-item" :class="{'disabled' : currentPage === lastPage}"><a @click.prevent="getProjects(currentPage + 1)" class="page-link" href="#">Next</a></li>
      </ul>
    </nav>
  </div>
</template>

<style lang="scss" scoped></style>
