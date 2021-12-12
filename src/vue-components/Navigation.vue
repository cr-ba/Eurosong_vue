<template>
    <nav class="c-nav">
        <span>
            {{ companyName }}
        </span>

      <ul class= "c-nav-list">
        <li class="c-nav-list-item" v-for="(link, index) in links" v-bind:key="index">
            <a v-bind:href="link.linkUrl">
                {{ link.linkText }}
            </a>
        </li>

        <li class="c-nav-list-item">
          Contact
        </li>
      </ul>
    </nav>
</template>

<script>
export default {
  name: 'Navigation',
  data() {
      return {
        companyName: "eurovision",
        links: [
            {
                linkText: "home",
                linkUrl: "/home"
            },
            {
                linkText: "contact",
                linkUrl: "/contact"
            }
        ]
      }
  }
}
</script>