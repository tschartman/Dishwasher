<template>
  <div data-app class="grocery">
    <Grocery/>
  </div>
</template>

<script>
// @ is an alias to /src
import Grocery from '@/components/Grocery.vue'

export default {
  name: 'Home',
  components: {
    Grocery
  }
}
</script>
