<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <transition name="flip" mode="out-in">
                    <component :is="mode" :counter="counter" :question="next" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Answer from './components/Answer.vue';
    import Score from './components/Score.vue';
    export default {
        data() {
            return {
                mode: 'app-question',
                counter:0,
                next:0
            }
        },
        methods: {
          reset(){
                this.counter=0;
                this.next=0;
          },
            check(next){
                if(next==10)
                {
                    
                  
                    var ans=this.counter;
                    alert('Your Score  : '+ ans)
                    alert('New Quiz')
                    this.reset();
                    this.mode='app-question';
                    return 1;
                }
                return 0
            },
          answered(isCorrect) {
              if (isCorrect) {
                  this.counter++
                  this.next++;
                  if(!this.check(this.next))
                  this.mode = 'app-answer';
              } else {
                  this.next++;
                  if(!this.check(this.next))
                  this.mode = 'app-score';
              }
          }
        },
        components: {
            appQuestion: Question,
            appAnswer: Answer,
            appScore: Score
        }
    }
</script>

<style>
    .flip-enter {
        transform: rotateY(0deg);
    }

    .flip-enter-active {
        animation: flip-in  0.5s ease-out forwards;
    }

    .flip-leave {
        transform: rotateY(0deg);
    }

    .flip-leave-active {
        animation: flip-out 0.5s ease-out forwards;
    }

    @keyframes flip-out {
        from {
            transform: rotateY(0deg);
        }
        to {
            transform: rotateY(90deg);
        }
    }

    @keyframes flip-in {
        from {
            transform: rotateY(90deg);
        }
        to {
            transform: rotateY(0deg);
        }
    }
</style>
