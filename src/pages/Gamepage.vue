<template>
    <div>
      <button @click="goToPage('home')">  
        go to home
      </button>
      <h1>
        Game
      </h1>

      <Carousel
        :items="songs"
        :activeIndex="activeSongIndex"

        @change-index="changeActiveSongIndex" 
      />

      <div v-for="(vote,index) in votes" :key="index">
          <button @click="addVote(vote.points)" v-if="!vote.isVoted">
            Add {{vote.points}} points
          </button>
      </div>

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
            songs: [],
            activeSongIndex: 0,
            votes: [
              {
                points: 1,
                isVoted: false

              },
              {
                points: 2,
                isVoted: false

              },
              {
                points: 4,
                isVoted: false

              },
              {
                points: 8,
                isVoted: false

              }
            ]
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
          },

          postVote(points) {
            const songId = this.songs[this.activeSongIndex].id;
            const url = "http://webservies.be/eurosong/Votes";
            
            fetch(url, {
              method: "POST",
              headers: {
                'Accept': 'application/json, text/plain',
                'Content-Type': 'application/json;charset=UTF-8'
              },
              body: JSON.stringify({
                songID: songId,
                points: points,
              })
            }).then((response) => {
              return response.json()
            }).then((result) => {
              console.log(result)
            })
          },


          changeActiveSongIndex(index) {
            this.activeSongIndex = index;
          },

          addVote(points) {
            let votes = this.votes;

            //create new array
            votes.map((vote) => {
              if(vote.points == points) {
                vote.isVoted = true;
              }
              return vote;
            });

            //post it to the api
            this.postVote(points);

            //check if all votes are set to true OR there are nog 'false' votes
            let activeVotes = votes.filter((vote) => vote.isVoted == true);
            
            //if everything is voted, redirect to ranking
            if (activeVotes.length == votes.length) {
              this.goToPage("ranking");
            }
          }

        }
    }
</script>
