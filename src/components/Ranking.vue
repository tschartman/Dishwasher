<template>
  <div class="ranking">
    <v-simple-table>
    <template v-slot:default>
    <thead>
        <tr>
        <th class="text-left">
            Name
        </th>
        <th class="text-left">
            Times Taken Trash
        </th>
        </tr>
    </thead>
    <tbody>
        <tr
        v-for="item in count"
        :key="item.name"
        >
        <td>{{ collectors[item.key] }}</td>
        <td>{{ item.count }}</td>
        </tr>
    </tbody>
    </template>
    </v-simple-table>
  </div>
</template>
<script>
export default {
  name: 'Trash',
  props: ['collectors', 'count'],
  data() {
    return {
    }
  },
  methods: {
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  
</style>
