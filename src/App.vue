<template>
  <div id="app">
    <Navigation/>
    <h1>
      Eurosong festival
    </h1>
    <Counter/>

    <Feedback 
      v-for="(message, index) in messages"
      :key = "index"
      :message="message.message"
      :classType="message.classType"
    />

    <button>
      Add message
    </button>

  </div>
</template>

<script>
import Navigation from "./vue-components/Navigation.vue";
import Counter from './vue-components/Counter.vue';
import Feedback from './vue-components/Feedback.vue';


//import whole styling for the app
import style from './scss/style.scss';

export default {
  name: 'App',
  components: {
    Navigation,
    Counter,
    Feedback
  },
  data() {
    return {
      messages: [
        {
          message: "error, tis kapot",
          classType: "warning"
        },
        {
          message: "great succes",
          classType: "succes"
        },
        {
          message: "test",
          classType: "test"
        }
      ]
    }
  }
}
</script>


