<template>
  <div class="p-3 rounded" style="max-width:400px; background-color:#0096c7; margin:25px auto">
    
    <!-- Input window -->
    <div class="w-full font-weight-bold rounded bg-vue-light my-2" style="height:150px; text-align:right;margin-right:5px">


      <div class="sum"
        style="text-align:right;margin-right:5px;color: black;font-size: 36px;align-items: center;padding-top: 25px;">
        {{newValue + operator + calcValue || 0}}
      </div>
      <!-- Output Sum -->
      <div class="sum" style="text-align:right;margin-right:5px;color: lightslategray;font-size: 24px;">
        {{overall || 0}}
      </div>

    </div>
    <!-- buttons -->
    <div class="row no-gutter">
      <div v-for="c in calculatorElements" :key="c" class="col-3">
        <div class="lead text-black text-right py-2 my-2 bg-vue-light rounded-circle hover-class"
          @click='handleInput(c)'>
          {{c}}
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
  name: "Home",
    components:{},
    setup() {
        const calcValue = ref("");
      const calculatorElements = ref(["C", "%", "/", "*", 7, 8, 9, "-", 4, 5, 6, "+", 1, 2, 3, "=", 0, "."]);
        const operator = ref("");
        const newValue = ref("");
        const overall = ref("");
        const percentValue = ref('')
        const handleInput = c => {
            if (!isNaN(c) || c==='.') {
              calcValue.value += c;
            }
            if (c === "C") {
                calcValue.value = "";
                overall.value = "";
                operator.value = "";
                newValue.value = "";
            }
            if (c === "%") {
              // calcValue.value = calcValue.value / 100;
              if (calcValue.value && newValue.value && operator.value) {
                overall.value = (calcValue.value / 100) * newValue.value
              }
              if (calcValue.value && !newValue.value) {
                overall.value = calcValue.value / 100
              }
            }
            if (["/", "*", "-", "+"].includes(c)) {
                operator.value = c;
                newValue.value = calcValue.value;
                calcValue.value = "";
            }
            if (c === "=") {
                overall.value = (eval(newValue.value + operator.value + calcValue.value)).toString();
           
                operator.value = "";
                newValue.value = "";
                calcValue.value = "";
            }
        };
        return {
            calculatorElements,
            calcValue,
            handleInput,
            overall,
            newValue,
            operator
        };
    },
}
</script>

<style>
.bg-vue-light {
  background: antiquewhite;
}

.hover-class:hover {
  background: lightgrey;
  cursor: pointer;
}

</style>
