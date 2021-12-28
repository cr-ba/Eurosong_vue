<template>
    <div>
      <button @click="goToPage('home')">  
        go to home
      </button>
      <h1>
        Ranking
      </h1>
      <div>
        <ul v-for="post in votes" v-bind:key="post.id">
          <li>Song: {{ post.title }}</li>
          <li>Number of votes: {{ post.points }}</li>
          <iframe :src="post.spotify" width="30%" height="80" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"></iframe>
        </ul>
      </div>
      <!-- <div id="app">
        {{ votes }}
    </div> -->
    </div>
</template>


<script>
    //songs/id/points gebruiken
    export default {
        name: "Rankingpage",
        data() {
          return {
            votes: [],
            //points: null,
            points: [],
            //votes : null,
            //artists: [],
          };
        },
        mounted() {
          //eerst votes oproepen
          this.fetchVotes();
        },
        methods: {
          goToPage(page) {
            this.$emit("change-page", page);
          },
        
        //get all votes
          fetchVotes() {
          const url = "http://webservies.be/eurosong/Songs";

          fetch(url)
            .then((response) => {
              return response.json();
              
            })
            .then((votes) => {
              this.votes = votes;         //in votes array zetten
            })
            .then((points) => {
              this.fetchPoints(points);
            })

          },
          fetchPoints() {

            this.votes.forEach((element, index) => {
              //console.log(element.id)
              
              fetch("http://webservies.be/eurosong/Songs/" + element.id +"/points")
              .then((response) => {
                return response.json();
              })
              .then((points) => {
                this.votes[index].points = points;         //in votes array zetten
                //console.log(points);
              })
            })
            //werkt niet???
            votes.sort(function (a, b) {
            return a.points - b.points;
            })

          },

        }
    }
</script>
