<template>
    <div>
      <h1>
        Eurosong voting app
      </h1>

      <button @click="goToPage('game')">  
        show game
      </button>

      <button @click="goToPage('ranking')">  
        show ranking
      </button>
    </div>
</template>

<script>
    export default {
        name: "Homepage",
        methods: {
            goToPage(page) {
                this.$emit("change-page", page);
            }
        }
    }
</script>
