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
          <li>{{ post.id }}</li>
          <li>{{ post.title }}</li>
          <li>{{ post.points }}</li>
        </ul>
      </div>
      <div id="app">
        {{ votes }}
    </div>
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
          };
        },
        mounted() {
          //eerst votes oproepen
          this.fetchVotes();
          //this.fetchPoints();
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
              return response.json()
              
            })
            .then((votes) => {
              //console.log(JSON.stringify(votes));
              this.votes = votes;         //in votes array zetten
            })
            .then((points) => {
              this.fetchPoints(points);
            })

          },
          fetchPoints() {
            //const url = "http://webservies.be/eurosong/Songs/" + 1 +"/points";//1,2,3,4,5
            //console.log(url);
            //console.log(this.votes[0].id);

            this.votes.forEach((element, index) => {
              //console.log(element.id)
              //console.log("http://webservies.be/eurosong/Songs/" + element.id +"/points")
              
              fetch("http://webservies.be/eurosong/Songs/" + element.id +"/points")
              .then((response) => {
                return response.json()
              })
              .then((points) => {
                //console.log(JSON.stringify(votes));
                //points.push(this.points)
                this.votes[index].points = points;         //in votes array zetten
                console.log(points);

                //points.push(points)
            })

            });
          }

          
        }
    }
</script>
