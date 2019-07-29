<template>
<div id="app" class="quiz" v-cloak>
  <div class="container">
    <div class="quiz__wrapper">
      <div
        v-for="( item, index ) in quiz.questions"
        class="quiz__question">
        <div
          class="quiz__question-box"
          v-show="index === questionIndex">
          <strong class="quiz__question-title">{{ item.text }}</strong>
          <div class="quiz__inputs-wrapper">
            <p
              v-for="( data, i ) in item.responses"
              class="quiz__question-input"
              :class="{ 'quiz__question-input_state-active ':data.isChecked }"
              @click="inputsToggle( data, i)"
              >
              {{ data.text }}
              <span
                class="quiz__checkbox"
                :class="{ 'quiz__checkbox_state-active ':data.isChecked }"
                ></span>
            </p>
          </div>
        </div>
      </div>
      <button
        @click="next"
        class="quiz__next-button">
        Далее
      </button>
    </div>
  </div>
</div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {

  components: {
    Logo
  },
  el: '#app',
  data () {
    return {
      quiz: {
        title: 'What superhero are you?',
        questions:
          [
            {
              text: "How would you describe your personality?",
              responses: [{
                  id: 0,
                  text: 'Im serious and dark',
                  value: 'Batman',
                  isChecked: false,
                },
                {
                  id: 1,
                  text: 'Arrogant, but charming',
                  value: 'Superman',
                  isChecked: false,
                },
                {
                  id: 2,
                  text: 'Fun and easy going',
                  value: 'The Flash',
                  isChecked: false,
                }
              ]
            },
            {
              text: "Why did you want to become a superhero?",
              responses: [{
                  id: 1,
                  text: 'For the thrills',
                  value: 'The Flash',
                  isChecked: false,
                },
                {
                  id: 2,
                  text: 'For justice',
                  value: 'Batman',
                  isChecked: false,
                },
                {
                  id: 3,
                  text: 'For popularity',
                  value: 'Superman',
                  isChecked: false,
                }
              ]
            },
          ]
      },
      questionIndex: 0,
      userResponses: Array()
    }
  },
  methods: {
    inputsToggle ( data, i ) {

      // let arr = this.menuLists;
      // arr.forEach( function( item ) {
      //   setTimeout( () =>
      //     item.isVisible = !item.isVisible
      //   , item.dataFade );
      // } );
      console.log(data.isChecked);
      console.log(i);
      return data.isChecked = !data.isChecked;
    },
    // Go to next question
    next () {
        this.questionIndex++;
        console.log(this.userResponses);
    },
    // Go to previous question
    prev () {
        this.questionIndex--;
    },
  }
}
</script>

<style>
#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

#app > .row {
  background: #fff;
}

h1 {
  margin-bottom: 20px;
}

[v-cloak] {
  display: none;
}
</style>
