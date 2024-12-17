<template>
  <div class="row">
    <div class="col-md-4" v-for="game in games" :key="game.id">
      <div>
        <div class="card" style="width: 18rem;">
       <img :src="game.background_image" class="card-img-top" alt="...">
       <div class="card-body">
       <h5 class="card-title">{{game.name}}</h5>
       <p class="card-text"> Rating {{ game.rating }}
        <span v-html="generateStars(game.rating)"></span>
       </p>
       <p class="card-text"> Released {{ game.released }}</p>
       <p class="card-text"> Updated {{ game.updated }}</p>
       <a href="#" class="btn btn-primary" @click="redirectOpinion(game.name)">Opinar</a>
      </div>
    </div>
      </div>
       
    </div>
  </div>
</template>

<script>


export default {
  name: 'home-vue',
  // props: {},
  data: function(){
    return {
      games:[]
    }
  },
  // computed: {},
  methods: {
    async fetchGames()
    {
      const apiKey = '5397cb3f472b462d9e59434349a1e8d2';
      const baseUrl = 'https://api.rawg.io/api/games?key=';
      const response= await fetch(baseUrl+apiKey)
      //verificar si existe error
      if (!response.ok)
      {
       throw new Error('error al obtener datos')

      }
      const data= await response.json()
      console.log(data)
      this.games= data.results
     
    },

    redirectOpinion(name) {
      this.$router.push('/opinion/'+name)
    },

    generateStars(rating) {
    const maxStars = 5; // Máximo número de estrellas
    const fullStars = Math.floor(rating); // Estrellas completas
    const halfStar = rating % 1 >= 0.5 ? 1 : 0; // Media estrella
    const emptyStars = maxStars - fullStars - halfStar; // Estrellas vacías

    return '⭐'.repeat(fullStars) + '⭐'.repeat(halfStar).replace('⭐', '⭐') + '☆'.repeat(emptyStars);
  }

    

    

    
  },
  // watch: {},
  // components: {},
  // mixins: [],
  // filters: {},
  // -- Lifecycle Methods
  created(){
    this.fetchGames()
  }

  // -- End Lifecycle Methods
}
</script>

<style scoped>
.row {
  display: flex; 
  justify-content: flex-start; 
  flex-wrap: wrap; 
  margin: 0 auto; 
}

.col-md-4 {
  margin-top: 20px; 
  display: flex; 
  justify-content: center; 
}

.card {
  margin: 0 auto;
}

  
</style>