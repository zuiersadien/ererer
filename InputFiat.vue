<script setup lang="ts">
import { ref, onMounted } from 'vue'
// import IMask from 'imask'
import { FiatCurrencyType } from '/@src/components/advanced/CalculatorExchange/CalculatorExchange.vue'

export interface InputFiatProps {
  label: string
  currencies: [FiatCurrencyType]
  fiatAmount: string
  tcPenUsd: string
}

withDefaults(defineProps<InputFiatProps>(), {
  label: '',
  currencies: () => ['USD'],
  fiatAmount: '',
  tcPenUsd: '',
})

let currencySelected = ref<FiatCurrencyType>('USD')
const inputOneValue = ref()

onMounted(() => {
  let defaultValue = currencies.value[0].id
  currencySelected.value = defaultValue
  emitFiatCurrency(defaultValue)
  // IMask(document.getElementById('phone-mask'), {
  //   mask: Number,
  //   decimal: '.',
  //   min: 0,
  //   max: 9999999,
  // })
})

/*
export default {
  name: 'InputFeat',
  props: ['label', 'currencies', 'fiatAmount', 'tcPenUsd'],
  data: () => ({
    currencySelected: null,
  }),
  computed: {
    classButtonPEN: function () {
      return {
        'btn-primary': this.currencySelected === 'PEN',
      }
    },
    classButtonUSD: function () {
      return {
        'btn-primary': this.currencySelected === 'USD',
      }
    },
  },
  mounted: function () {
    this.init()
    IMask(document.getElementById('phone-mask'), {
      mask: Number,
      decimal: '.',
      min: 0,
      max: 9999999,
    })
  },
  methods: {
    init() {
      let defaultValue = this.currencies[0].id
      this.currencySelected = defaultValue
      this.emitFiatCurrency(defaultValue)
    },
    emitFiatCurrency(value) {
      this.currencySelected = value
      this.$emit('fiatCurrency', value)
    },
    emitFiatAmount(e) {
      this.$emit('fiatAmount', e.target.value)
    },
  },
}
*/
</script>

<template>
  <div style="height: 170px">
    <div class="exchange-box">
      <div class="selector">
        <p class="text">{{ label }}</p>
        <div class="coin">
          <div class="language-select">
            <button
              class="btn btn-sm"
              :class="classButtonPEN"
              @click="emitFiatCurrency('PEN')"
            >
              Soles
            </button>
            <button
              class="btn btn-sm"
              :class="classButtonUSD"
              @click="emitFiatCurrency('USD')"
            >
              Dólares
            </button>
          </div>
        </div>
      </div>
      <div class="form-group">
        <VInput v-model="inputOneValue" placeholder="John Doe" />
        <label>{{ inputOneValue }}</label>
      </div>
      <small v-if="currencySelected === 'PEN'">
        Tipo de cambio: S/ {{ tcPenUsd.toFixed(3) }}
      </small>
    </div>
  </div>
</template>
