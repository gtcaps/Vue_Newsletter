<template>
    <div class="main-container">
        <h3>Noticias reales, para humanos reales</h3>
        <span>Todas las categorias existentes para que siempre estes actualizado y en constante aprendizaje.</span>

        <div class="card-container d-flex flex-wrap justify-content-between">
            <!--<Card   v-for="a in data" :key="a.id" :titulo ="a.title" :ruta="a.image" :descripcion="a.description"></Card>-->
            <Card   v-for="a in arr" v-if="a.subscribed >= Number(a.target)"  :key="a.id" :titulo ="a.title" :ruta="a.image" :descripcion="a.description"></Card>
        </div>

        <hr>
        <br>
        <h3>Proximas Categorias</h3>
        <span>Si deseas que agreguemos una categoria porque es de ayuda para ti, vota por tus favoritas</span>

        <div class="card-container d-flex flex-wrap justify-content-between">
            <!--<Card   v-for="a in data" :key="a.id" :titulo ="a.title" :ruta="a.image" :descripcion="a.description"></Card>-->
            <VoteCard   
                v-for="a in arr" 
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
import Card from '@/components/Card'
import VoteCard from '@/components/VoteCard.vue'

export default {
  components:{
    Card,
    VoteCard
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
          data: [],
          arr: [
              {
                  image: "https://images.pexels.com/photos/2917442/pexels-photo-2917442.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Web Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 200,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/830891/pexels-photo-830891.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Android Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 100,
                  target: "200"
              },
              {
                  image: "https://images.pexels.com/photos/373076/pexels-photo-373076.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "IOS Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 99,
                  target: "0"
              },
              {
                  image: "https://images.pexels.com/photos/1089438/pexels-photo-1089438.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "React Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 50,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/267350/pexels-photo-267350.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Software Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 180,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/1482476/pexels-photo-1482476.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Vue Development",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 200,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/2599244/pexels-photo-2599244.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Java EE",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 20,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/842554/pexels-photo-842554.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "JAVA SE",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 35,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/699122/pexels-photo-699122.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Data Structures",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 40,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/1626481/pexels-photo-1626481.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Algorithms",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 190,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/2918011/pexels-photo-2918011.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
                  title: "Computational Thinking",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 160,
                  target: "100"
              },
              {
                  image: "https://images.pexels.com/photos/2922379/pexels-photo-2922379.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260",
                  title: "Internet of Things",
                  description: "Passage its ten led hearted removal cordial. Preference any astonished unreserved mrs. .",
                  subscribed: 400,
                  target: "100"
              }
          ]
      }
  },

  created(){
      this.getData();
      console.log(this.arr);
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