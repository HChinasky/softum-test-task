<template>
  <div class="vld-parent">
    <loading
        v-model:active="isLoading"
        :is-full-page="fullPage"
        color="#0d6efd"
        :opacity="1"/>
  </div>
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Выберите дату</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="d-flex flex-wrap">
            <div class="col-12 col-md-6">
              <datepicker
                  :disabled-dates="disabledDates"
                  v-model="date"
                  name="currencyDate">
                <template v-slot:belowDate>
                  <span></span>
                </template>
              </datepicker>
            </div>
            <div class="col-12 col-md-6">
              <select class="form-select border-dark shadow-none" v-model="currency">
                <option value="usd">USD</option>
                <option value="eur">EUR</option>
                <option value="rub">RUB</option>
                <option value="pln">PLN</option>
                <option value="gbp">GBP</option>
              </select>
            </div>
          </div>
        </div>
        {{ infoCurrency }}
        <div class="modal-footer">
          <button
              data-bs-dismiss="modal"
              type="button"
              class="btn btn-primary"
              :disabled="isDisabled"
              @click="getInfoCurrency">
            Проверить
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs3-datepicker'
import { ref } from 'vue'
import moment from 'moment'
import router from '@/router'
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.css';

export default {
  name: 'ModalComponent',
  components: {
    Datepicker,
    Loading
  },
  data() {
    return {
      currency: null,
      infoCurrency: null,
      isLoading: false,
      fullPage: true
    }
  },
  setup() {
    let currentDate = new Date()
    currentDate.setFullYear(currentDate.getFullYear() - 2) // Subtracting 2 years

    const date = ref(new Date())
    const disabledDates = {
      to: currentDate, // Disable all dates up to specific date
      from: new Date(), // Disable all dates after specific date
    }
    return {date, disabledDates}
  },
  computed: {
    isDisabled: function () {
      return !this.currency;
    }
  },
  methods: {
    getInfoCurrency: async function () {
      const formatDate = moment(this.date).format('DD.MM.YYYY')
      this.isLoading = true;

      await this.axios
          .get('http://localhost:8080/p24api/exchange_rates?json&date=' + formatDate) // fixed cors error for local
          .then(response => {
                this.isLoading = false
                router.push(
                    {
                      name: 'result',
                      params: {
                        data: JSON.stringify(response.data.exchangeRate),
                        date: formatDate,
                        currency: this.currency
                      }
                    }
                )
              }
          )
    }
  }
}
</script>

<style lang="scss">
.form-select {
  padding: 11px !important;
}
</style>
