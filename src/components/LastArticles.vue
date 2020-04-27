<template>
  <div class="general">
    <SliderComponent texto="Bienvenido al curso de Vue" home="true"></SliderComponent>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Últimos artículos</h2>

        <!--Listado articulos-->
       <div id="articles">
          <Articles v-bind:articles="articles"></Articles>
        </div>
      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SliderComponent from "./SliderComponent.vue";
import SidebarComponent from "./SidebarComponent.vue";
import Global from "../Global";
import Articles from "./Articles.vue"


export default {
  name: "LastArticles",
  components: {
    SliderComponent,
    SidebarComponent,
    Articles
  },
  mounted() {
    this.getLastArticles();
  },
  data() {
    return {
      url: Global.url,
      articles: null
    };
  },
  methods: {
    getLastArticles() {
      axios.get(this.url+"/articles/true").then(res => {
        if (res.data.status == "success") {
          this.articles = res.data.articles;

          console.log(this.articles);
        }
      });
    }
  }
};
</script>
