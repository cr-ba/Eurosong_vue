<template>
    <div>
      <button @click="goToPage('home')">  
        go to home
      </button>
      <h1>
        Game
      </h1>

      <!-- <div v-for="song in songs" :key="song.id"> 
        {{song.artist.name}} - {{song.title}}
      </div> -->

      <Carousel
        :items="songs"
      />
    </div>
</template>

<script>
//components
import Carousel from '../vue-components/Carousel.vue';

    export default {
        name: "Gamepage",
        components: {
          Carousel
        },
        data() {
          return {
            songs: []
          }
        },
        mounted() {
          //eerst songs oproepen
          this.fetchSongs();
        },
        methods: {
          //navigation method
            goToPage(page) {
                this.$emit("change-page", page);
            },
            
          //data methods
          
          //get all songs
          fetchSongs() {
          const url = "http://webservies.be/eurosong/Songs";

          fetch(url)
            .then((response) => {
              return response.json();
            })
            .then((songs) => {
              //vanuit deze functie artists oproepen
              this.fetchArtists(songs);
            });
          },
          
          //get artists
          fetchArtists(songs) {
          const url = "http://webservies.be/eurosong/Artists";

          fetch(url)
            .then((response) => {
              //response is text so convert to json
              return response.json();
            })
            .then((artists) => {
              //loop over array songs with forEach method
              songs.map((song) => {
                //find the artists in array
                const artist = artists.find((artist) => artist.id == song.artist);

                //Replace id by artist object
                song.artist = artist;

                //return the new object
                return song;
              });

              //change data of songs so everything will get rerendered
              this.songs = songs;
              //console.log(songs);
            });
          }
        }
    }
</script>
