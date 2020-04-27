<template>
  <div class="general">
    
    <div class="center">
      <section id="content">
        <h1 class="subheader">Películas</h1>

        <div class="mis-datos" v-if="misDatos">
            <p v-html="misDatos"></p>
            <br/>
            {{ web | mayusculas | concatenaYear('Esta es la fecha!')}}
        </div>

        <div class="favorita" v-if="favorita">
          La película marcada es:
          <h2>{{favorita.title}}</h2>
        </div>

        <!--Listado peliculas-->
        <div id="articles">
          <!-- -->
          <div v-for="pelicula in peliculasMayuscula" v-bind:key="pelicula.title">
            <Pelicula 
                      :pelicula="pelicula"
                      @favorita="haLlegadoLaPeliculaFavorita"></Pelicula>
          </div>
        </div>
      </section>
      <SidebarComponent></SidebarComponent>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import Pelicula from "./Pelicula.vue";
import SidebarComponent from './SidebarComponent.vue'
export default {
  name: "Peliculas",
  components: {
    Pelicula,
    SidebarComponent
  },
  methods: {
    haLlegadoLaPeliculaFavorita(favorita){
        this.favorita = favorita;
    }
  },
  filters: {
    mayusculas(value) {
      return value.toUpperCase();
    },
    concatenaYear(value, message){
      var fecha = new Date();
      return value + ' ' + fecha.getFullYear() + ' ' + message;
    }
  },
  computed: {
    peliculasMayuscula(){
        var peliculasMod = this.peliculas;
        for(var i = 0; i < this.peliculas.length; i++){
          peliculasMod[i].title = peliculasMod[i].title.toUpperCase();
        }

        return peliculasMod;
    },
    misDatos(){
      return this.nombre + ' ' + this.apellido + '<br/>' + '<strong>Sitio web: </strong>' + this.web;
    }

  },
  data() {
    return {
      nombre: 'Carlos',
      apellido: 'Britos',
      web: 'https://charliebp1mycurriculum.000webhostapp.com/',
      favorita: null,
      peliculas: [
        {
          title: "Batman vs Superman",
          year: 2016,
          image:
            "https://dam.smashmexico.com.mx/wp-content/uploads/2018/04/24160545/batman_v_superman_dawn_of_justice-cover-770x433.jpg"
        },
        {
          title: "Gran Torino",
          year: 2008,
          image:
            "http://diariobasta.com/wp-content/uploads/2019/08/grantorino-708x350@2x.jpg"
        },
        {
          title: "El señor de los anillos",
          year: 2003,
          image:
            "https://3.bp.blogspot.com/-Z9_SOccupGU/VwUv6htiHSI/AAAAAAAAKUw/zNE2zzTYInM3Pw9fJK6B6ZSe4wmlvn_FQ/s640/El-Se%25C3%25B1or-de-los-Anillos-La-Comunidad-del-Anillo.jpg"
        },
        {
          title: "Sonic la película",
          year: 2020,
          image:
            "https://1.bp.blogspot.com/-yCe4DWZSngg/XdduHX75SqI/AAAAAAAAhtA/Yi9ecHwbcSMIHQX2V8kqxifqeSfC9Q8pQCLcBGAsYHQ/s2560/sonic-the-hedgehog-2020-movie-9u-2560x1440.jpg"
        }
      ]
    };
  }
};
</script>
