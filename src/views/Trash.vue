<template>
  <div class="dishwasher">
    <Trash/>
  </div>
</template>

<script>
// @ is an alias to /src
import Trash from '@/components/Trash.vue'

export default {
  name: 'Home',
  components: {
    Trash
  }
}
</script>
