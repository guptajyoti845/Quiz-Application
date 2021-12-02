<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{width:`${(questionAnswered / questions.length) * 100}%`}"></div>
      <div class="status">{{ questionAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <transition-group name="fade">
      <div
          class="single-question"
          v-for="(question, index) in questions"
          :key="question"
          v-show="questionAnswered===index"
      >
        <div class="question">{{ question.q }}</div>
        <div
            class="answers"
            v-for="answer in question.answers"
            :key="answer"
            @click.prevent="selectAnswer(answer.is_correct)"
        >
          <div class="answer">{{ answer.text }}</div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "questions",
  props: {
    questions: {
      default: []
    },
    questionAnswered: {
      default: ''
    }
  },
  emits: ['question-answered'],
  methods: {
    selectAnswer(is_correct) {
      this.$emit('question-answered', is_correct)
    }
  },
}
</script>

<style scoped>

</style>
