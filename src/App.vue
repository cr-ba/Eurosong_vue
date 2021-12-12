<template>
  <div id="app">
    <nav class="c-nav">
      <ul class= "c-nav-list">
        <li class="c-nav-list-item">
          Home
        </li>

        <li class="c-nav-list-item">
          Contact
        </li>
      </ul>
    </nav>
    <!-- content -->
    <h1>
      Eurosong festival
    </h1>

    <div class="c-feedback warning">
      fout gebeurd
    </div>
    <div class="c-feedback error">
      tis kapot
    </div>
    <div class="c-feedback succes">
      het werkt
    </div>
  </div>
</template>

<script>
//import whole styling for the app
import style from './scss/style.scss';

export default {
  name: 'App'
}
</script>


