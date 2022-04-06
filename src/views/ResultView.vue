<template>
  <HeaderComponent header-title="Результат" />
  <div class="container mt-4">
    <h6>Курс за - {{ this.$route.params.date }}</h6>
    <h6>Выбранная валюта - <span class="text-uppercase">{{ this.$route.params.currency }}</span></h6>
    <div class="d-flex flex-wrap">
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс продажу НБУ (saleRateNB) - <span class="text-primary">{{ findCurrency.saleRateNB }}</span>, <span class="text-success">{{ sumValue(findCurrency.saleRateNB).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.saleRateNB).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс купівлі НБУ (purchaseRateNB) - <span class="text-primary">{{ findCurrency.purchaseRateNB }}</span>, <span class="text-success">{{ sumValue(findCurrency.purchaseRateNB).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.purchaseRateNB).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс продажу ПриватБанку (saleRate) - <span class="text-primary">{{ findCurrency.saleRate }}</span>, <span class="text-success">{{ sumValue(findCurrency.saleRate).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.saleRate).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс купівлі ПриватБанку (purchaseRate) - <span class="text-primary">{{ findCurrency.purchaseRate }}</span>, <span class="text-success">{{ sumValue(findCurrency.purchaseRate).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.purchaseRate).checkNumber }}</span></p>
      </div>
    </div>
    <router-link class="btn btn-primary mt-3" to="/">Вернуться на главную</router-link>
  </div>
</template>

<script>
import HeaderComponent from '@/components/base/HeaderComponent'

export default {
  name: 'ResultView',

  components: {
    HeaderComponent
  },
  computed: {
    findCurrency: function () {
      const parseDate = JSON.parse(this.$route.params.data)
      return parseDate.find(e => e.currency === this.$route.params.currency.toUpperCase());
    }
  },
  methods: {
    sumValue: function (val) {
      const strArr = val.toString().split("");
      let sum = 0
      for(let i = 0; i < strArr.length; i++) {
        if(Number(strArr[i])){
          sum += Number(strArr[i])
        }
      }

      const checkNumber = this.checkNumberPair(sum)
      return {sum, checkNumber}
    },
    checkNumberPair: function (num) {
      return num % 2 ? false : true
    }
  }
}
</script>