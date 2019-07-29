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
          <div
            v-if="item.tag == 'List'"
            class="quiz__inputs-wrapper">
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
          <div
            v-else-if="item.tag == 'Price'"
            class="quiz__inputs-wrapper">
            <input
              class="quiz__input-range"
              type="range"
              min="75" max="1000"
              step="10"
              v-model="priceValue"
              >
            <p
              class="quiz__question-input"
              v-text="total"></p>
          </div>
        </div>
      </div>
      <button
        @click="prev"
        class="quiz__prev-button"
        v-show="questionIndex > 0"
        >

        Назад
      </button>
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
              text: "Для каких целей вам нужен хостинг?",
              tag: 'List',
              responses: [{
                  id: 0,
                  text: 'Блог',
                  value: 'Host-1',
                  isChecked: false,
                },
                {
                  id: 1,
                  text: 'Посадочная страница',
                  value: 'Host-A',
                  isChecked: false,
                },
                {
                  id: 2,
                  text: 'Сайт-галерея',
                  value: 'Host-B',
                  isChecked: false,
                },
                {
                  id: 3,
                  text: 'Персональная страница',
                  value: 'Host-0',
                  isChecked: false,
                },
                {
                  id: 4,
                  text: 'Cайт компании',
                  value: 'Host-3',
                  isChecked: false,
                },
                {
                  id: 5,
                  text: 'Форум',
                  value: 'VIP-1',
                  isChecked: false,
                },
                {
                  id: 6,
                  text: 'Крупный e-commerce',
                  value: 'VIP-3',
                  isChecked: false,
                }
              ]
            },
            {
              text: "Какая CMS?",
              tag: 'List',
              responses: [{
                  id: 1,
                  text: 'Wordpress',
                  value: 'Wordpress',
                  isChecked: false,
                },
                {
                  id: 2,
                  text: 'Joomla',
                  value: 'Joomla',
                  isChecked: false,
                },
                {
                  id: 3,
                  text: '1С-Битрикс',
                  value: '1С-Битрикс',
                  isChecked: false,
                },
                {
                  id: 4,
                  text: 'Drupal',
                  value: 'Drupal',
                  isChecked: false,
                },
                {
                  id: 5,
                  text: 'Никакая',
                  value: 'No',
                  isChecked: false,
                }
              ]
            },
            {
              text: "Обслуживание в год/рублей",
              tag: 'Price',
              responses:
                [
                  {
                    from: 100,
                    to: 1000,
                  }
                ]


              //   [{
              //     id: 1,
              //     text: 'От',
              //     value: 100,
              //     isChecked: false,
              //   },
              //   {
              //     id: 2,
              //     text: 'до',
              //     value: 1000,
              //     isChecked: false,
              //   },
              // ]
            },
          ]
      },
      questionIndex: 0,
      userResponses: Array(),
      priceValue: 100,
    }
  },
  computed: {
    total () {
      return this.priceValue;
    }
  },
  methods: {
    inputsToggle ( data, i ) {
      data.isChecked = !data.isChecked;
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

<style lang="scss">
@import "~/assets/sass/base/_variables.scss";
@import "~/assets/sass/base/_settings.scss";
@import "~/assets/sass/base/_mixins.scss";
@import "~/assets/sass/base/_variables.scss";

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.quiz {

  padding: 10px;

  &__wrapper {
    height: 450px;
    height: 450px;
    // background: #eee;
  }

  &__question-title {
    margin-bottom: 20px;
    display: block;
  }

  &__inputs-wrapper {
    padding: 25px 0;
  }

  &__question-input {
    position: relative;
    padding: 15px 0 15px 35px;
    cursor: pointer;

    &_state-active {
      color: #278272;
    }
  }

  &__checkbox {
    position: absolute;
    left: 0;
    top: 11px;
    width: 24px;
    height: 24px;
    background: #fff;
    border: 3px solid #9e9e9e;

    &_state-active {

      border: 3px solid #000;

      &:before {
        content: '';
        position: absolute;
        left: 2px;
        width: 15px;
        height: 10px;
        border-left: 2px solid;
        border-bottom: 2px solid;
        transform: rotate(-45deg);
      }
    }
  }

  &__question-box {
    transition: all .4s ease-in-out;
  }

  &__next-button {
    padding: 10px 20px;
    color: #fff;
    cursor: pointer;
    background-color: #278272;
    border: none;
    font-size: 18px;
  }

  &__prev-button {
    margin-right: 3px;
    padding: 7px 20px;
    color: #000;
    cursor: pointer;
    background-color: #365cb500;
    border: none;
    outline: 3px solid;
    font-size: 18px;
    transition: all .4s ease-in-out;
  }
}

input[type=range] {
  -webkit-appearance: none;
  margin: 18px 0;
  width: 310px;
}
input[type=range]:focus {
  outline: none;
}
input[type=range]::-webkit-slider-runnable-track {
  width: 310px;
  height: 4px;
  cursor: pointer;
  animate: 0.2s;
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: $button_color;
  border-radius: 1.3px;
  border: 0.2px solid #010101;
}
input[type=range]::-webkit-slider-thumb {
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  border: 1px solid #000000;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -14px;
}
input[type=range]:focus::-webkit-slider-runnable-track {
  background: $button_color;
}
input[type=range]::-moz-range-track {
  width: 310px;
  height: 4px;
  cursor: pointer;
  animate: 0.2s;
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  background: $button_color;
  border-radius: 1.3px;
  border: 0.2px solid #010101;
}
input[type=range]::-moz-range-thumb {
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  border: 1px solid #000000;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
}
input[type=range]::-ms-track {
  width: 310px;
  height: 4px;
  cursor: pointer;
  animate: 0.2s;
  background: transparent;
  border-color: transparent;
  border-width: 16px 0;
  color: transparent;
}
input[type=range]::-ms-fill-lower {
  background: $button_color;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type=range]::-ms-fill-upper {
  background: $button_color;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type=range]::-ms-thumb {
  // box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  border: 1px solid #000000;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
}
input[type=range]:focus::-ms-fill-lower {
  background: $button_color;
}
input[type=range]:focus::-ms-fill-upper {
  background: $button_color;
}

[v-cloak] {
  display: none;
}
</style>
