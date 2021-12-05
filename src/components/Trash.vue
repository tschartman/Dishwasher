<template>
  <div class="trash">
    <h1>Trash Collector:</h1>
        <div v-if="collector !== null">
            <h2 class="collector">{{collectors[collector]}}</h2>
        </div>
        <div v-else class="collector">
            <h3>loading...</h3>
        </div>
        <div class="update">
            <div @click="remindCollector()" class="button remind">Remind</div>
            <div @click="updateCollector(false)" class="button skip">Skip</div>
            <div @click="updateCollector(true)" class="button completed">I Took It</div>
        </div> 
    <br>
    <h2>Ranking</h2>
    <Ranking :collectors="collectors" :count="count" />
  </div>
</template>

<script>
import axios from 'axios'
import Ranking from '@/components/Ranking.vue'

export default {
  name: 'Trash',
  components: {
      Ranking
  },
  data() {
    return {
      collector: null,
      collectors: null,
      count: null,
    }
  },
  methods: {
      remindCollector() {
        axios.get('https://dishwasher-api.herokuapp.com/trash/notify')
      },
      async updateCollector(completed) {
          const keys = Object.keys(this.collectors)
          const nextCollector = (this.collector + 1) % keys.length
          const response = await axios.post('https://dishwasher-api.herokuapp.com/trash/collector', {collector: nextCollector, completed})
          if (response.data.acknowledged) {
              if (completed) {
                  this.updateCount(this.collector)
              }
              this.collector = nextCollector
          }
      },
      updateCount(collector) {
          const newCount = [...this.count];
          const updatedIndex = newCount.findIndex((keys) => keys.key === collector);
          newCount[updatedIndex].count += 1;
          this.count = newCount;
      }
  },
  async mounted () {
    const {data: {count}} = await axios.get('https://dishwasher-api.herokuapp.com/trash/count')
    const {data: {collectors}} = await axios.get('https://dishwasher-api.herokuapp.com/collectors')
    const response = await axios.get('https://dishwasher-api.herokuapp.com/trash/collector')
    this.collector = response.data.collector
    this.collectors = collectors
    this.count = count
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.collector {
    width: 200px;
    padding: 30px 10px 30px 10px;
    background-color: goldenrod;
    margin: auto;
    border-radius: 6px;
    margin-top: 20px;
    color: honeydew;
}

.update {
    margin-top: 20px;
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

.skip {
    background-color: mediumseagreen;
}

.completed {
    background-color: slateblue;
}

.remind {
    background-color: salmon;
}
  
</style>
