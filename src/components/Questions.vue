<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnsweered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnsweered }} out of {{ questions.length }} questions
        answered
      </div>
    </div>

    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, index) in questions"
        :key="question.q"
        v-show="questionsAnsweered === index"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Questions",
  emits: ["question-answered"],
  props: ["questions", "questionsAnsweered"],

  setup(_, { emit }) {
    const selectAnswer = (is_correct) => {
      emit("question-answered", is_correct);
    };

    return {
      selectAnswer,
    };
  },
};
</script>

<style scoped></style>
