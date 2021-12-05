<template>
  <div class="hello">
    <h1>The Dishwasher is</h1>
    <div v-if="clean === null"><h2>Loading...</h2></div>
    <div v-else class="square" :class="{clean: clean, dirty: !clean}">
      <h2>{{clean ? 'Clean' : 'Dirty'}}</h2>
    </div>
    <br>
    <h2>Change?</h2>
    <div class="update">
      <div @click="updateStatus(true)" class="button clean">It's Clean</div>
      <div @click="updateStatus(false)" class="button dirty">It's Dirty</div>
    </div> 
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Dishwasher',
  data() {
    return {
      clean: null
    }
  },
  methods: {
   async updateStatus(clean) {
      const res = await axios.post('https://dishwasher-api.herokuapp.com/washer/update', {clean});
      if (res.data.acknowledged) {
        this.clean = clean
      }
    }
  },
  async mounted () {
    const res = await axios.get('https://dishwasher-api.herokuapp.com/washer/status');
    this.clean = res.data[0].clean
  } 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .square {
    display: flex;
    justify-content: center;
    color: honeydew;
    width: 20%;
    padding: 75px;
    text-align: center;
    margin: auto;
    border-radius: 6px;
    margin-top: 50px;
  }

  .update {
    display: flex;
    justify-content: center;
  }

  .button {
    cursor: pointer;
    color: honeydew;
    padding-left: 50px;
    padding-right: 50px;
    padding-top: 20px;
    padding-bottom: 20px;
    border-radius: 6px;
    margin: 10px;
  }

  .clean {
    background-color: darkgreen;
  }

  .dirty {
    background-color: maroon;
  }
</style>
