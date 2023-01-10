<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<script>
import { computed } from "vue";

export default {
  name: "Result",
  props: ["results", "totalCorrect"],
  setup(props) {
    const resultIndex = computed(() => {
      let index = 0;

      props.results.forEach((element, i) => {
        if (
          element.min <= props.totalCorrect &&
          element.max >= props.totalCorrect
        ) {
          index = i;
        }
      });

      return index;
    });

    return {
      resultIndex,
    };
  },
};
</script>

<style scoped></style>
