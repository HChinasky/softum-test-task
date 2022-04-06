<template>
  <div class="navbar bg-primary justify-content-center">
    <h1 class="text-white text-center">{{ headerTitle }}</h1>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
  props: {
    headerTitle: {
      type: String
    }
  }
}
</script>