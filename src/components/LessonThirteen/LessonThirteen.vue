<template>
  <div id="app">
    <b-container fluid>
      <h3 class="text-center"><img src="https://codemoji.com/images/white-logo.png" class="codemoji-logo"> Lesson 13 of 17</h3>
      <b-progress>
        <b-progress-bar height="25px" :value="value" :max="max" variant="success" animated>{{value}}%</b-progress-bar>
      </b-progress>
    </b-container>
    <br>

    <b-container fluid>
      <b-row>

        <b-col class="col-md-3 d-flex align-items-stretch">

            <b-card header="Lesson Instructions"
                header-tag="header" style="min-width: 100%">
              <b-form-textarea plaintext style="width: 100%; height: 100%;" value="Now we know how to put our data inside an array. But how will we access it?

Every element in an array gets assigned a number. As you read the data from left to right, a number is assigned starting from zero. So the array [“hello”, “sir”, 4] would have each element represented by a number. “Hello” is assigned 0, “sir” is assigned 1, and the number 4 is assigned 2. As we add more elements to the array, the numbers continue to increment up by 1

We can access these elements by using bracket notation after declaring the variable. For example:

Var myArray = [“hello”, “sir”, 4]

We get a value from the array like this:

Var greeting = myArray[0]

In this example, greeting would return “hello”

Let’s give this a try by looking at a variable containing all different types of food. We're going to grab pizza from the food array so we will make the variable myLunch equal to pizza
This is our food variable: var food = ['pizza', 'hamburger', 'sandwich'];
"
></b-form-textarea>
        </b-card>
          </b-col>

          <b-col class ="col-md-5 d-flex align-items-stretch">
            <b-card header="Chef Leo is here to help! Follow his instructions below!"
                header-tag="header">
              <b-container>
                <b-row>
                  <b-col class="col-md-3"><img class="chef" src="../../../cartoonchef.png"></b-col>
                  <b-col class="col-md-9">
                    <b-list-group>
                      <b-list-group-item>
                        Access the first element of this array with a variable called myLunch
                        To access an element in an array, write the name of the array, put square brackets after that,
                        and put the number of the element that you're trying to access.
                      </b-list-group-item>
                    </b-list-group>
                  </b-col>
                </b-row>
              </b-container>
              <md-card>
                <md-card-media>
                  <div class="codemirror">
                    <codemirror v-model="code" :options="cmOption"></codemirror>
                  </div>
                </md-card-media>
              </md-card>
              <button class="btn btn-success btn-block" @click="checkAnswer">Ok! Check my code!</button>
              <b-btn @click="showReset" variant="danger" block>Reset</b-btn>
            </b-card>
          </b-col>

          <b-col class="col-md-4 d-flex align-items-stretch">
            <b-card header="Chef's Table"
                header-tag="header">
              <div class="text-center parent">
                <transition name="fade" mode="out-in">
                  <img v-if="pizza" class="pizza" src="../../../pizza.jpg">
                </transition>

                <img class="cuttingboard" src="../../../cuttingboard.png">
              </div>
              <div class="card-footer">
                <b-btn v-if="pizza" @click="changeLesson" variant="success" class="btn-block pulse-button">Next lesson <i class="fas fa-arrow-right"></i></b-btn>
              </div>
            </b-card>
          </b-col>

      </b-row>
    </b-container>


<div>
  <b-modal v-model ="showLessonDetails" hide-footer title="Codemoji JavaScript">
      <div class="d-block text-center">
        <h4>Lesson 13: Accessing data from an array</h4>
      </div>
    Now we know how to put our data inside an array. But how will we access it?

    Every element in an array gets assigned a number. As you read the data from left to right, a number is assigned starting from zero. So the array [“hello”, “sir”, 4] would have each element represented by a number. “Hello” is assigned 0, “sir” is assigned 1, and the number 4 is assigned 2. As we add more elements to the array, the numbers continue to increment up by 1

    We can access these elements by using bracket notation after declaring the variable. For example:

    Var myArray = [“hello”, “sir”, 4]

    We get a value from the array like this:

    Var greeting = myArray[0]

    In this example, greeting would return “hello”

    Let’s give this a try by looking at a variable containing all different types of food. We're going to grab pizza from the food array so we will make the variable myLunch equal to pizza<br>
    This is our food variable: var food = ['pizza', 'hamburger', 'sandwich'];
    <b-btn class="mt-3" variant="success" block @click="showLessonDetails=!showLessonDetails">Ok, got it!</b-btn>
    </b-modal>
    <b-modal ref="myModalRef" hide-footer title="Codemoji JavaScript">
      <div class="d-block text-center">
        <h4>Great job! </h4>
      </div>
      <b-btn class="mt-3" variant="success" block @click="showPizza">Submit and show animation</b-btn>
    </b-modal>

    <b-modal ref="myErrorRef" hide-footer title="Codemoji Objects">
      <div class="d-block text-center">
        <h4>Hmm, that's not quite right</h4>
      </div>
      <p>{{ errorMessage }}</p>
      <b-btn class="mt-3" variant="danger" block @click="hideError">Let me try again!</b-btn>
    </b-modal>

  <b-modal ref="resetRef" hide-footer title="Codemoji Objects">
    <div class="d-block text-center">
      <h4>Are you sure you want to reset your code?</h4>
    </div>
    <b-row>
      <b-btn class="mt-3" variant="danger" block @click="resetCode"style="width: 50%">Yes, reset my code</b-btn>
      <b-btn class="mt-3" block variant="primary" style="width: 50%" @click="hideReset">No, let me keep trying!</b-btn>
    </b-row>
  </b-modal>
  </div>
  <p v-if="showAnswer">Answer: var myLunch = food[0];</p>
  </div>
</template>

<script>
import Output from "./Output";
export default {
  data() {
    return {
      code: ``,
      showAnswer: false,
      counter: 0,
      showAlert: false,
      showOnloadModal: true,
      answer: 'varmyLunch=food[0];',
      value: 81,
      max: 100,
      showLessonDetails: true,
      errorMessage: '',
      pizza: false,
      cmOption: {
        styleActiveLine: false,
        lineNumbers: true,
        line: true,
      }
    }
  },
  components: {
    appOutput: Output
  },
  methods: {
    changeLesson () {
      this.$refs.myModalRef.hide()
      this.$ga.event({
        eventCategory: 'lessonChange',
        eventAction: 'action',
        eventLabel: 'nextLesson',
        eventValue: 14
      })
      this.$emit('lessonChanged')
    },
    resetCode () {
      this.code = ``
      this.errorMessage = ''
      this.$refs.resetRef.hide()
    },
    showPizza () {
      this.pizza = true;
      this.$refs.myModalRef.hide();
    },
    showModal () {
      this.$refs.myModalRef.show()
    },
    hideModal () {
      this.$refs.myModalRef.hide()
    },
    showError() {
      this.$refs.myErrorRef.show();
    },
    hideError() {
      this.$refs.myErrorRef.hide();
      this.errorMessage = ''
    },
    showReset() {
      this.$refs.resetRef.show()
    },
    hideReset() {
      this.$refs.resetRef.hide()
    },
    checkAnswer() {
      let potentialAnswer = this.code.split('');
      let myAnswer =[]
      //removes spaces from code so that students won't get errors for spacing
      for(let i = 0; i < potentialAnswer.length; i++) {
        if (potentialAnswer[i] !== " "&& potentialAnswer[i] !== '\n') {
          myAnswer.push(potentialAnswer[i]);
        }
      }

        if (myAnswer[0]+myAnswer[1]+myAnswer[2] !== 'var') {
        this.errorMessage = "Looks like you either forgot to type 'var' or misspelled it, go back and try again!";
      } else if(myAnswer[3]+myAnswer[4]+myAnswer[5]+myAnswer[6]+myAnswer[7]+myAnswer[8]+myAnswer[9] !== 'myLunch') {
        this.errorMessage = "Looks like you forgot to type 'myLunch' or misspelled it, go back and try again!";
      } else if (myAnswer[10]!=='=') {
        this.errorMessage = "Looks like you missed your equals sign after your variable name. Place one there and try again!"
      } else if(myAnswer[11]+myAnswer[12]+myAnswer[13]+myAnswer[14]!== 'food') {
          this.errorMessage = "Don't forget to type the name of the array we're accessing. It's called 'food'"
      } else if (myAnswer[15] !== '[') {
        this.errorMessage = "Looks like you missed the first square bracket. Add it and try again!"
      } else if(myAnswer[16]!== "0") {
        this.errorMessage = "Remember, every item in an array gets assigned a number starting from 0. We are trying to access the first item in the food array"
      } else if(myAnswer[17] !== ']') {
        this.errorMessage = "Looks like you forgot your second square bracket. Try again!"
      } else if(myAnswer[18] !== ';') {
        this.errorMessage = "Don't forget your semi colon!"
        }
      myAnswer= myAnswer.join('');
      if(this.errorMessage === '') {
        this.showModal();
      } else {
        this.showError();
        myAnswer = []
        this.counter++
      }
    }
  }
}
</script>

<style>

.parent {
  position: relative;
  top: 0;
  left: 0;
}
.CodeMirror {
  height: 250px
}

.cuttingboard {
  width: 93%;
  position: relative;
  top: 0;
  left: 0;
  z-index: 0;
}

.pizza {
  position: absolute;
  margin-top: 70px;
  margin-left: 60px;
  top: 0;
  left: 0;
  z-index: 1;
  width: 60%;
}
.pulse-button {
  position: relative;
  border: none;
  box-shadow: 0 0 0 0 green;
  background-size: cover;
  background-repeat: no-repeat;
  cursor: pointer;
  -webkit-animation: pulse 2s infinite cubic-bezier(0.3, 0, 0, 1);
  -moz-animation: pulse 2s infinite cubic-bezier(0.3, 0, 0, 1);
  -ms-animation: pulse 2s infinite cubic-bezier(0.3, 0, 0, 1);
  animation: pulse 2s infinite cubic-bezier(0.3, 0, 0, 1);
}
.pulse-button:hover {
  -webkit-animation: none;
  -moz-animation: none;
  -ms-animation: none;
  animation: none;
}

@-webkit-keyframes pulse {
  to {
    box-shadow: 0 0 0 10px rgba(232, 76, 61, 0);
  }
}
@-moz-keyframes pulse {
  to {
    box-shadow: 0 0 0 10px rgba(232, 76, 61, 0);
  }
}
@-ms-keyframes pulse {
  to {
    box-shadow: 0 0 0 10px rgba(232, 76, 61, 0);
  }
}
@keyframes pulse {
  to {
    box-shadow: 0 0 0 10px rgba(232, 76, 61, 0);
  }
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.fade-enter {
        opacity: 0;
    }
    .fade-enter-active {
        transition: opacity 0.5s;
    }
    .fade-leave-active {
        transition: opactiy 0.5s;
        opacity: 0;
    }
.chef {
  width: 75%;
}
</style>
