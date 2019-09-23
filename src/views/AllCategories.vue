<template>
    <div class="main-container">
        <h3>Noticias reales, para humanos reales</h3>
        <span>Todas las categorias existentes para que siempre estes actualizado y en constante aprendizaje.</span>

        <div class="card-container d-flex flex-wrap justify-content-between">
            <Card  v-for="a in data" :key="a.id" :titulo ="a.title" :ruta="a.image" :descripcion="a.description"></Card>
        </div>

    </div>
</template>


<script>
import Card from '@/components/Card'

export default {
  components:{
    Card
  },

  methods:{
      getData() {
      const url = process.env.VUE_APP_API + "/newsletters";
      axios.get(url)
        .then(response => {
          console.log(response.data);
          this.data = response.data;
        })
        .catch(() => {
          alert("Hubo un error");
        });
    }
  },

  data: () => {
      return{
          data: []
      }
  },

  created(){
      this.getData();
  }
}
</script>


<style scoped>

.main-container{
    width: 80%;
    min-height: 100vh;
    margin: 0 auto;
    padding-top: 50px;
}

.card-container{
    margin-top: 30px;
    width: 100%;

}

</style>