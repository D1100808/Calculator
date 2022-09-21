<template>
<div class="p-3 rounded" style="max-width:400px; background-color:#0096c7; margin:25px auto">
    <!-- Input window -->
    <div class="w-full font-weight-bold rounded bg-vue-light my-2"
        style="height:150px; text-align:right;margin-right:5px">


        <div class="dollar d-flex bd-highlight"
            style="text-align:left;margin-right:5px;color: black;font-size: 20px;align-items: center;padding-top: 25px;">
            <p class="p-2 flex-grow-1 bd-highlight">доллар США USD ></p>
            <p class="p-2 flex-grow-1 bd-highlight">{{dollarValue || 0}}</p>
        </div>
        <!-- Output Sum -->
        <div class="tenge d-flex bd-highlight" style="text-align:left;margin-right:5px;color: black;font-size: 20px;align-items: center;padding-top: 5px;">
            <p class="p-2 flex-grow-2 bd-highlight">Казахстанский тенге KZT ></p>
            <p class="p-2 flex-grow-1 bd-highlight">{{currency || 0}}</p>
        </div>

    </div>
    <!-- buttons -->

    <div class="row row-cols-3 no-gutter">
        <div v-for="e in exchange" :key="e" class="col">
            <div class="lead text-black text-right py-2 my-2 bg-vue-light rounded-circle hover-class"
                @click='handleOutput(e)'>
                {{e}}
            </div>
        </div>
    </div>


</div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { watchEffect } from '@vue/runtime-core'
export default {
    setup() {
        const exchange = ref(['C', '.', 'x',7,8,9,4,5,6,1,2,3,0])
        const dollarValue = ref('')
        const currency = ref('');
        const error = ref(null);
        const handleOutput = e => {
            if (!isNaN(e) || e === '.') {
                dollarValue.value += e
            }
            if (e === 'C') {
                dollarValue.value = ''
            }
            if (e === 'x') {
                dollarValue.value = dollarValue.value.slice(0, -1)
            }
        }

        const getCurrency = async () => {
            
                let res = await fetch(
                    "http://openexchangerates.org/api/latest.json?app_id=a80029082e1f432db95a8579307c1eb2"
                )
                    .then(response => response.json())
                    .then(data => currency.value = data.rates.KZT.toFixed(1))
                    .catch(err => error.value = err.message)
        };
        watchEffect(() => {
            if (dollarValue) {
                getCurrency()
                currency.value*=dollarValue.value
            } else {
                currency.value = ''
            }
        })
        

        return { exchange, dollarValue, handleOutput,currency }
    }
}
</script>

<style>
</style>
