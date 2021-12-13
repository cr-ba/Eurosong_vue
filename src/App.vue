<template>
  <div id="app">
    <!-- homepagina -->
    <Homepage
    v-if="page=='home'"

    @change-page="goToPage"
    />

    <!-- game -->
    <Gamepage
    v-if="page=='game'"

    @change-page="goToPage"
    />

    <!-- ranking -->
    <Rankingpage
    v-if="page=='ranking'"

    @change-page="goToPage"
    />

  </div>
</template>

<script>
import Homepage from "./pages/Homepage.vue";
import Gamepage from "./pages/Gamepage.vue";
import Rankingpage from "./pages/Rankingpage.vue";

export default {
  name: 'App',
  components: {
    Homepage,
    Gamepage,
    Rankingpage
  },
  data() {
    return {
      page: "game"
    }
  },
  methods: {
    goToPage(page) {
      this.page = page;
    }
  }
}
</script>


