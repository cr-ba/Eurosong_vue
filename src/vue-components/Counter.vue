<template>
    <div>
        Buttoncounter: {{count}}
        <button @click="addOne">
            add 1
        </button>

        <button @click="minOne">
            min 1
        </button>
    </div>
</template>

<script>
export default {
  name: 'Counter',
  data() {
        return {
            count:0
        }
  },
  methods: {
      addOne() {
          this.count++;
      },
      minOne() {
          this.count--;
      }
  }
}
</script>
