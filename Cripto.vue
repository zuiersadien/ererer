<script setup lang="ts">
import { number } from "@intlify/core-base";
import IMask from 'imask';

import {defineProps, inject ,ref,defineEmits ,onMounted} from "vue"

defineProps({
valor:String
}
    
)
 const emit=defineEmits(["modificarValor"])
 

    const handleClose = (e) => {
        emit('modificarValor',e.target.value)
        
    }

onMounted(()=>{
    IMask(document.getElementById('phone-mask'), {
            mask: Number,
            decimal : ".",
            min: 0,
            max: 9999999,
        });

})
</script>

<template>

    <Field>
          <FieldLabel type="hero" label="Recibes"></FieldLabel>
          <Control>
         <input maxlength="10"  placeholder="24.30" class="input is-rounded size-lg"  rounded size="lg" id="phone-mask"  type="text" :value="valor" v-on:keyup="handleClose"/>
          </Control>
        </Field>



</template>

<style scoped lang="scss">

</style>