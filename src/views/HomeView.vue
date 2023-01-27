<template>
  <home />
</template>

<script>
import { defineComponent } from "vue";

// Components
import home from "../components/Home.vue";

export default defineComponent({
  name: "HomeView",

  components: {
    home,
  },
});
</script>
