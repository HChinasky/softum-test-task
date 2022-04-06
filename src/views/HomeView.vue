<template>
  <HeaderComponent header-title="Добро пожаловать"/>
  <div class="container">
    <div class="mt-4 d-flex justify-content-center">
      <button
          type="button"
          class="btn btn-success text-white text-uppercase"
          data-bs-toggle="modal"
          data-bs-target="#exampleModal">
        выбрать дату
      </button>
    </div>
  </div>
  <ModalComponent />
</template>

<script>
import ModalComponent from '@/components/ModalComponent'
import HeaderComponent from '@/components/base/HeaderComponent'

export default {
  name: 'HomeView',
  components: {
    ModalComponent,
    HeaderComponent
  }
}
</script>
