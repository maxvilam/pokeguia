<template>
  <div id="app">
    <h1>{{ titulo }}</h1>
    <img src="../public/titulo.png" width="300" height="auto" alt="" />
    <div class="container">
      <div class="row">
        <div class="col-12"><h1>PokeGuía</h1></div>
        <div class="col-12"></div>
        <div class="col-12">
          Nombre:
          <input type="text" v-model="pokemon" />
          <button class="btn-success" @click="buscaPoke">Buscar</button>
        </div>
        <div
          class="col-12"
          v-if="DataPoke.sprites.other.dream_world.front_default"
        >
          <img
            class="mt-3 border formatimg"
            :src="imgPoke"
            alt=""
            width="200px"
          />
        </div>
        <div class="mt-3 col-12">
          <h4>Movimientos</h4>
          <p class="mt-0 mb-0" v-for="(movimiento, i) of moviPoke" :key="i">
            * {{ movimiento.move.name }} *
          </p>
        </div>
        <div class="mt-3 col-12">
          <h4>Habilidades</h4>
          <p class="mt-0 mb-0" v-for="(habilidad, i) of habilidadPoke" :key="i">
            * {{ habilidad.ability.name }} *
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pokemon: "pikachu",
      URL: "https://pokeapi.co/api/v2/pokemon/",
      DataPoke: {},
      imgnoencontrado: "src/assets/img/noencontrado.jpg",
    };
  },
  created() {
    this.obtenerPoke();
  },
  computed: {
    titulo() {
      const titulo = "Busqueda de Pokemones";
      return titulo.toUpperCase();
    },
    moviPoke() {
      return this.DataPoke?.moves;
    },
    habilidadPoke() {
      console.log(this.DataPoke.abilities);
      return this.DataPoke?.abilities;
    },

    nombrePoke() {
      return this.DataPoke?.name;
    },
    imgPoke() {
      return this.DataPoke?.sprites.other.dream_world.front_default;
    },
  },
  methods: {
    async obtenerPoke() {
      try {
        const req = await fetch(`${this.URL}${this.pokemon.toLowerCase()}`);
        const data = await req.json();
        this.DataPoke = data;
      } catch (error) {
        const pordefecto = "metapod";
        alert("Personaje no encontrado");
        console.log(error);
        this.pokemon = pordefecto;
        this.obtenerPoke();
      }
    },
    buscaPoke() {
      this.obtenerPoke();
    },
  },
};
</script>

<style lang="scss">
#app {
  background-image: url(../public/fondo.jpg);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}
.clase1 {
  color: red;
}
.clase2 {
  color: blue;
}
.clase2 {
  color: green;
}

.formatimg {
  background-color: gray;
  border-radius: 50px;
  box-shadow: 20px 20px 50px yellowgreen;
}
</style>
