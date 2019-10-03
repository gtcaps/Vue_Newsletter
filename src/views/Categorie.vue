<template>
    <div class="main-container">
        <h3>Noticias reales, para humanos reales</h3>
        <span>Todas las categorias existentes para que siempre estes actualizado y en constante aprendizaje.</span>

        <div class="card-container d-flex flex-wrap justify-content-around">
            <Card   
                v-for="a in data"
                :key="a.id" 
                :titulo ="a.title" 
                :ruta="a.image" 
                :descripcion="a.description"
                :news_id="a.id"
                ></Card>
        </div>

        <hr>
        <br>
        <h3>Proximas Categorias</h3>
        <span>Si deseas que agreguemos una categoria porque es de ayuda para ti, vota por tus favoritas</span>

        <div class="card-container d-flex flex-wrap justify-content-around">
            <!--v-if="a.subscribed < Number(a.target)"-->
            <VoteCard   
                v-for="a in data" 
                v-if="a.subscribed < Number(a.target)"  
                :key="a.id" 
                :titulo ="a.title" 
                :ruta="a.image" 
                :descripcion="a.description" 
                :votos=a.subscribed 
                :objetivo="a.target"
            ></VoteCard>
        </div>

    </div>
</template>


<script>
import Card from "@/components/Card";
import VoteCard from "@/components/VoteCard.vue";

export default {
  components: {
    Card,
    VoteCard
  },

  methods:{
      getData() {
      const url = process.env.VUE_APP_API + "/tags/"+this.categorie+"?include=newsletters";
      axios.get(url)
        .then(response => {
          this.data = response.data.newsletters;
        })
        .catch(() => {
          alert("Hubo un error");
        });
    }
  },

  data: () => {
    return {
      data: [],
      categorie: ""
    };
  },

  watch: {
    $route() {
      this.categorie = this.$route.params.slug;
      this.getData();
    }
  },

  created(){
    this.categorie = this.$route.params.slug;
    this.getData();
  }

};
</script>



<style scoped>
.main-container {
  width: 80%;
  min-height: 81vh;
  margin: 0 auto;
  padding-top: 50px;
}

.card-container {
  margin-top: 30px;
  width: 100%;
}
</style>


