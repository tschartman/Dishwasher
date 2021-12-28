<template>
    <v-card
        class="list"
        max-width="500"
    >
    <v-toolbar
        color="red"
        dark
    >
        <v-toolbar-title>Grocery List</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon>
            <v-icon @click="$emit('openForm')">mdi-plus</v-icon>
        </v-btn>
    </v-toolbar>
    <template v-for="(item, index) in items">
        <v-list-item :key="item._id">
            <v-list-item-content>
                <v-list-item-title>{{item.name}}</v-list-item-title>
            </v-list-item-content>
                <v-list-item-action>
                    <v-btn icon>
                        <v-icon color="grey lighten-1" @click="$emit('deleteItem', item)">mdi-delete</v-icon>
                    </v-btn>
                </v-list-item-action>
        </v-list-item>
        <v-divider
        v-if="index < items.length - 1"
        :key="index"
    ></v-divider>
    </template>
</v-card>
</template>

<script>
  export default {
    name: 'Grocery',
    props: ['items', 'openForm', 'deleteItem'],
    data: () => ({
    })

  }
     
  
</script>
<style scoped>
.list {
    margin: auto;
    margin-top: 20px;
}
</style>