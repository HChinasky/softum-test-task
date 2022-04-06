<template>
  <HeaderComponent header-title="Результат" />
  <div class="container mt-4">
    <h6>Курс за - {{ this.$route.params.date }}</h6>
    <h6>Выбранная валюта - <span class="text-uppercase">{{ this.$route.params.currency }}</span></h6>
    <div class="d-flex flex-wrap">
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс продажу НБУ - <span class="text-primary">{{ findCurrency.saleRateNB }}</span>, <span class="text-success">{{ sumValue(findCurrency.saleRateNB).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.saleRateNB).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс купівлі НБУ - <span class="text-primary">{{ findCurrency.purchaseRateNB }}</span>, <span class="text-success">{{ sumValue(findCurrency.purchaseRateNB).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.purchaseRateNB).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс продажу ПриватБанку - <span class="text-primary">{{ findCurrency.saleRate }}</span>, <span class="text-success">{{ sumValue(findCurrency.saleRate).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.saleRate).checkNumber }}</span></p>
      </div>
      <div class="border-bottom w-100 mt-3">
        <p class="mb-0">Курс купівлі ПриватБанку - <span class="text-primary">{{ findCurrency.purchaseRate }}</span>, <span class="text-success">{{ sumValue(findCurrency.purchaseRate).sum }}</span>, <span class="text-warning">{{ sumValue(findCurrency.purchaseRate).checkNumber }}</span></p>
      </div>
    </div>
    <router-link class="btn btn-primary mt-3" to="/">Вернуться на главную</router-link>
  </div>
</template>

<script>
import HeaderComponent from '@/components/base/HeaderComponent'

export default {
  name: 'ResultView',

  data() {
    return {
      curr: [
        {
          "baseCurrency": "UAH",
          "saleRateNB": 21.966,
          "purchaseRateNB": 21.966
        },
        {
          "baseCurrency": "UAH",
          "currency": "AZN",
          "saleRateNB": 17.2433,
          "purchaseRateNB": 17.2433
        },
        {
          "baseCurrency": "UAH",
          "currency": "BYN",
          "saleRateNB": 10.6335,
          "purchaseRateNB": 10.6335
        },
        {
          "baseCurrency": "UAH",
          "currency": "CAD",
          "saleRateNB": 23.4067,
          "purchaseRateNB": 23.4067
        },
        {
          "baseCurrency": "UAH",
          "currency": "CHF",
          "saleRateNB": 31.5332,
          "purchaseRateNB": 31.5332,
          "saleRate": 32.9,
          "purchaseRate": 31.3
        },
        {
          "baseCurrency": "UAH",
          "currency": "CNY",
          "saleRateNB": 4.5977,
          "purchaseRateNB": 4.5977
        },
        {
          "baseCurrency": "UAH",
          "currency": "CZK",
          "saleRateNB": 1.3228,
          "purchaseRateNB": 1.3228,
          "saleRate": 1.43,
          "purchaseRate": 1.23
        },
        {
          "baseCurrency": "UAH",
          "currency": "DKK",
          "saleRateNB": 4.3259,
          "purchaseRateNB": 4.3259
        },
        {
          "baseCurrency": "UAH",
          "currency": "EUR",
          "saleRateNB": 32.176,
          "purchaseRateNB": 32.176,
          "saleRate": 32.6,
          "purchaseRate": 32
        },
        {
          "baseCurrency": "UAH",
          "currency": "GBP",
          "saleRateNB": 38.3195,
          "purchaseRateNB": 38.3195,
          "saleRate": 40.1,
          "purchaseRate": 38.1
        },
        {
          "baseCurrency": "UAH",
          "currency": "GEL",
          "saleRateNB": 9.5417,
          "purchaseRateNB": 9.5417
        },
        {
          "baseCurrency": "UAH",
          "currency": "HUF",
          "saleRateNB": 0.087112,
          "purchaseRateNB": 0.087112
        },
        {
          "baseCurrency": "UAH",
          "currency": "ILS",
          "saleRateNB": 9.1199,
          "purchaseRateNB": 9.1199
        },
        {
          "baseCurrency": "UAH",
          "currency": "JPY",
          "saleRateNB": 0.23828,
          "purchaseRateNB": 0.23828
        },
        {
          "baseCurrency": "UAH",
          "currency": "KZT",
          "saleRateNB": 0.06256,
          "purchaseRateNB": 0.06256
        },
        {
          "baseCurrency": "UAH",
          "currency": "MDL",
          "saleRateNB": 1.5945,
          "purchaseRateNB": 1.5945
        },
        {
          "baseCurrency": "UAH",
          "currency": "NOK",
          "saleRateNB": 3.3724,
          "purchaseRateNB": 3.3724
        },
        {
          "baseCurrency": "UAH",
          "currency": "PLN",
          "saleRateNB": 6.937,
          "purchaseRateNB": 6.937,
          "saleRate": 7.18,
          "purchaseRate": 6.88
        },
        {
          "baseCurrency": "UAH",
          "currency": "RUB",
          "saleRateNB": 0.34775,
          "purchaseRateNB": 0.34775
        },
        {
          "baseCurrency": "UAH",
          "currency": "SEK",
          "saleRateNB": 3.0987,
          "purchaseRateNB": 3.0987
        },
        {
          "baseCurrency": "UAH",
          "currency": "SGD",
          "saleRateNB": 21.5522,
          "purchaseRateNB": 21.5522
        },
        {
          "baseCurrency": "UAH",
          "currency": "TMT",
          "saleRateNB": 8.3585,
          "purchaseRateNB": 8.3585
        },
        {
          "baseCurrency": "UAH",
          "currency": "TRY",
          "saleRateNB": 1.9897,
          "purchaseRateNB": 1.9897
        },
        {
          "baseCurrency": "UAH",
          "currency": "UAH",
          "saleRateNB": 1,
          "purchaseRateNB": 1
        },
        {
          "baseCurrency": "UAH",
          "currency": "USD",
          "saleRateNB": 29.2549,
          "purchaseRateNB": 29.2549,
          "saleRate": 29.5474,
          "purchaseRate": 29.2549
        },
        {
          "baseCurrency": "UAH",
          "currency": "UZS",
          "saleRateNB": 0.0025673,
          "purchaseRateNB": 0.0025673
        }
      ]
    }
  },
  components: {
    HeaderComponent
  },
  computed: {
    findCurrency: function () {
      return JSON.parse(this.$route.params.data).find(e => e.currency === this.$route.params.currency.toUpperCase());
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