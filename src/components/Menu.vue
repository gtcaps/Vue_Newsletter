<template>
  <div class="menu-container">
    <nav class="navbar navbar-light bg-transparent">
      <a class="navbar-brand d-flex logo-styles" href="#">
        <i class="far fa-newspaper"></i>[ INSIDE ]
      </a>
    </nav>
    <ul class="nav">
      <li class="nav-item">
        <router-link
          to="/"
          class="nav-link item-styles"
          :class="clicked == 'todas' ? 'selection' : ''"
          @click.native="hola('todas')"
        >Todas</router-link>
      </li>
      <li class="nav-item" v-for="a in tags" :key="a.id">
        <router-link
          to="/categorie"
          class="nav-link item-styles"
          @click.native="hola(a.id)"
          :class="clicked == a.id ? 'selection' : ''"
        >{{ a.name }}</router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Menu",

  created() {
    this.getData();
  },

  methods: {
    getData() {
      const url = process.env.VUE_APP_API + "/tags";
      axios.get(url)
        .then(response => {
          this.tags = response.data;
        })
        .catch(() => {
          alert("Hubo un error");
        });
    },

    hola(selectedItem) {
      this.clicked = selectedItem;
      this.$router.push();
    }
  },

  data: () => {
    return {
      tags: [],
      clicked: "todas"
    };
  }
};
</script>

<style scoped>
a.logo-styles {
  font-family: "Merriweather", serif;
  font-weight: bold;
  font-size: 1.45rem;
  color: tomato;
}

i {
  color: tomato;
  font-size: 2rem;
  margin-right: 10px;
}

.menu-container {
  border: 1px solid rgba(0, 0, 0, 0.1);
}

.item-styles {
  color: rgb(120, 120, 120);
}

.item-styles:hover {
  background: rgba(252, 228, 236, 0.5);
  color: black;
}

.selection {
  background: rgba(252, 228, 236, 0.5);
  color: black;
}
</style>