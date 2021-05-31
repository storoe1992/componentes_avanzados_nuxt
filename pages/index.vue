<template>
  <div id="app">
    <b-container>
    <b-navbar toggleable="lg" type="dark" variant="success">
      <b-navbar-brand href="#"><img  width="100px" src="../assets/img/1200px-Rick_and_Morty.svg.png" alt="Rick and Morty" class="img-fluid ms-4"></b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/cursos">Cursos</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <section class="main">
        <b-row my=5 id="resultados" class="my-5 mx-auto">
            <b-col cols="12" xl="4" lg="4" md=6  v-for="personaje in personajes" :key="personaje.id" class="text-center my-3">
                <b-card
                 :img-src="personaje.img"
                 img-alt="Image"
                 img-top
                 tag="article"
                 style="max-width: 18rem;"
                 class="mx-auto">
                  <b-card-text class="text-start">{{personaje.nombre}}</b-card-text>
                </b-card>
            </b-col>
        </b-row>
    </section>
    </b-container>
  </div>
</template>

<script>
import Personaje from '../classes/personaje'

export default {
  name: 'App',
  data() {
    return {
      personajes: []
    }
  },
  methods: {
    loadPersonajes : async (api) => {
        let resultCall = await fetch(api);
        let result = await resultCall.json();
        return result.results;
    }
  },
  created(){
    let url = 'https://rickandmortyapi.com/api/character';
    this.loadPersonajes(url).then(personajes => {
      personajes.forEach(personaje => {
        if(this.personajes.length != 5){
        let personajeToAdd = new Personaje(personaje.id,personaje.name,personaje.species,personaje.image);
        this.personajes.push(personajeToAdd);
        }
      });
      
    })
  }
}
</script>
