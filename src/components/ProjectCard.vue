<script>
import {store} from "../store";

export default {
    name: 'ProjectCard',
    props: {
        project: Object
    },
    data() {
        return {
            store
        }
    },
    computed: {
      descriptionPreview() {
        // se il contenuto è più lungo di 150 caratteri
        // prendo solo i primi 150 caratteri e aggiungo ...
        // altrimenti ritorno il contenuto
        if(!this.project.description) {
          return 'Nessuna descrizione'
        } else if(this.project.description.length > 150) {
          return this.project.description.substring(0, 150) + "...";
        } else {
          return this.project.description
        }
      },
      imgSrc() {
        // se il progetto inizia con https:// ritorna project.image
        // altrimenti ritorna ${store.apiBaseUrl}/storage/${project.image}
        if(!this.project.image) return "";
        if(this.project.image.startsWith('htpps://')) {
          return this.project.image;
        } else {
          return `${this.store.apiBaseUrl}/storage/${this.project.image}`;
        }
      }
    }
}
</script>

<template>
    <div class="card h-100">
        <img v-if="project.image" :src="imgSrc" class="card-img-top" :alt="project.title">
        <div v-else>
          Nessuna immagine presente
        </div>
          <div class="card-body">
            <h5>{{ project.title }}</h5>
            <p>{{ descriptionPreview }}</p>
            <router-link :to="{ name: 'single-project', params: { slug: project.slug }}" class="btn btn-primary">Leggi</router-link>
          </div>
        </div>
</template>

<style lang="scss" scoped>

</style>