<script setup lang="ts">
import { number } from "@intlify/core-base";
import {defineProps,defineExpose, onUnmounted ,toRefs,inject ,ref,defineEmits,onMounted ,computed} from "vue"
import IMask from 'imask';

const props=defineProps({
currencies:Array,
fiatAmount:Number,
tcPenUsd:Number
}
    
)
const { currencies } = toRefs(props);
// VARIABLES
    const currencySelected=ref("")
// 
// FUNTIONS
function emitFiatCurrency(value){
            currencySelected.value = value
           emit ('fiatCurrency', value)
           console.log(currencies.value)
        }
function emitFiatAmount(e){
            emit('fiatAmount', e.target.value)
             console.log(currencies.value)
        }

const  init=async()=>{
            let defaultValue =await currencies.value[0].id
            currencySelected.value = defaultValue
            emitFiatCurrency(defaultValue)
        }


// definir funciones
 const emit=defineEmits(["fiatAmount","fiatCurrency"])
 
// 
    
// Mounted
onMounted(()=>{
    init()
    IMask(document.getElementById('phone-mask1'), {
            mask: Number,
            decimal : ".",
            min: 0,
            max: 9999999,
        });

})
 


// 

//COMPUTED 
    const classButtonPEN=computed(()=>{
        return {
                'btn-primary': currencySelected.value === 'PEN',
            }
    }
    )
     const classButtonUSD=computed(()=>{
        return {
                'btn-primary': currencySelected.value === 'USD',
            }
    }
    )
// 

</script>

<template>
     <button v-on:click="emitFiatCurrency('PEN')" :class="classButtonPEN">Soles</button>

    <button v-on:click="emitFiatCurrency('USD')"  :class="classButtonUSD">Dólares</button>
 <Field>

          <FieldLabel type="hero" label="Tu nos envías"></FieldLabel>
          <Control>
         <input class="input is-rounded size-lg" id="phone-mask1" rounded   type="text" :value="fiatAmount" v-on:keyup="emitFiatAmount"/>

          </Control>
        </Field>

    <div>
<small v-if="currencySelected === 'PEN'">Tipo de cambio: S/ {{ tcPenUsd.toFixed(3) }}</small>
</div>



</template>

<style scoped lang="scss">

</style>