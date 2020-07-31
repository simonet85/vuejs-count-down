<template>
  <Counter
    :year="2020"
    :month="7"
    :date="1"
    :hour="0"
    :minute="0"
    :second="5"
    :millisecond="5"
  />
</template>

<script>
import Counter from "../components/Counter.vue";
export default {
  components: {
    Counter,
  },
};
</script>

<style lang="css" scoped></style>
