<template>
  <div class="dishwasher">
    <Dishwasher/>
  </div>
</template>

<script>
// @ is an alias to /src
import Dishwasher from '@/components/Dishwasher.vue'

export default {
  name: 'Home',
  components: {
    Dishwasher
  }
}
</script>
