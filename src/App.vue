<template>
  <div>
    <div class="header">
      <h1>Random Cat Gif</h1>
    </div>

    <form class="form" @submit.prevent="onSubmit">
      <div>
        <label>Título: </label>
        <input v-model="cat.title" placeholder="Ingrese un título">
        <br><br>
      </div>

      <div>
        <label for="filtro">Filtro: </label>
        <select v-model="cat.filter">
          <option selected v-for="(filter, $index) in filters" :key="$index"> {{ filter }} </option>
        </select>
        <br>
      </div>
      
      <div class="colorBlock">
        <label for="color">Color: </label>
        <select v-model="cat.color">
          <option selected v-for="(color, $index) in colors" :key="$index" :value="color.color"> {{ color.name }} </option>
        </select>
        <span v-if="cat.color === 'red'" class="dot" id="dotRed"></span>
        <span v-else-if="cat.color === 'blue'" class="dot" id="dotBlue"></span>
        <span v-else-if="cat.color === 'green'" class="dot" id="dotGreen"></span>
        <span v-else-if="cat.color === 'yellow'" class="dot" id="dotYellow"></span>
        <span v-else-if="cat.color === 'white'" class="dot" id="dotWhite"></span>
        <br><br>
      </div>
      
      <div>
        <label>Tamaño: </label>
        <input v-model="cat.size" type="number" step="100" min="100" max="900" placeholder="Ingrese un número">
        <br><br>
        <button type="submit">Obtener mi gatito</button>
      </div>
    </form>

    <div class="cat">
      <img :src="catGif">
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    catGif: "",
    cat: {
      title: "",
      filter: "",
      color: "",
      size: "",
    },
    filters: ['blur', 'mono', 'sepia', 'negative', 'paint'],
    colors: [
      {
        "color":"red",
        "name":"rojo",
      },
      {
        "color":"blue",
        "name":"azul",
      },
      {
        "color":"green",
        "name":"verde",
      },
      {
        "color":"yellow",
        "name":"amarillo",
      },
      {
        "color":"white",
        "name":"blanco",
      }
    ]
  }),
  
  methods: {
    onSubmit(){
      this.catGif = `https://cataas.com/cat/gif/says/${this.cat.title}?filter=${this.cat.filter}&color=${this.cat.color}&${this.cat.size}=40&type=or`
    }
  }

}
</script>

<style>
body, html {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100vh;
  background-color: lightskyblue;
}
h1 {
  margin: 0;
}
.header{
  padding: 30px;
}
.form {
  background-color: lightpink;
  padding: 20px;
}
.cat {
  padding: 20px;
}
.colorBlock {
  display: flex;
  align-items: center;
  justify-content: center;
  align-content: space-between
}
.dot {
  height: 25px;
  width: 25px;
  border-radius: 50%;
  display:inline-flex;
  margin-left: 5px;
}

#dotRed{
  background-color: red;
}
#dotBlue{
  background-color: blue;
}
#dotGreen{
  background-color: green;
}
#dotYellow{
  background-color: yellow;
}
#dotWhite{
  background-color: white;
}
</style>
