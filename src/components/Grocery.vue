<template>
  <v-container fluid>
    <v-row justify="center">
        <v-col>
            <GroceryList :items="items" @openForm="openForm" @deleteItem="deleteItem" /> 
        </v-col>
    </v-row>
    <v-dialog
        v-model="dialog"
        width="500"
    >
        <v-card>
            <v-card-title class="text-h5 grey lighten-2">
            Add Item
            </v-card-title>

            <v-card-text>
                <v-text-field
                    v-model="item"
                    label="Item"
                    required
                ></v-text-field>
            </v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
                color="primary"
                text
                @click="addItem()"
            >
                Add
            </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
  import axios from 'axios'
  import GroceryList from '@/components/GroceryList.vue'

  export default {
    name: 'Grocery',
    components: {
        GroceryList
    },
    data: () => ({
        items: [],
        item: '',
        dialog: false
    }),
    methods: {
        openForm() {
            this.dialog = true
        },
         async addItem() {
            const res = await axios.post('https://dishwasher-api.herokuapp.com/grocery', {name: this.item})
            if (res.data.acknowledged) {
                const newItems = [...this.items];
                newItems.push({name: this.item, _id: res.data.insertedId})
                this.items = newItems;
            }
            this.item = ''
            this.dialog = false
        },
        async deleteItem(item) {
            const res = await axios.delete('https://dishwasher-api.herokuapp.com/grocery', {data: {name: item.name}})
            console.log(item.name)
            if (res.data.acknowledged) {
                const newItems = [...this.items];
                const itemIndex = this.items.findIndex(i => i._id === item._id)
                newItems.splice(itemIndex)
                this.items = newItems
            }
        }
    },
    async created() {
        const res = await axios.get('https://dishwasher-api.herokuapp.com/grocery')
        this.items = res.data;
    }
  }
     
  
</script>
<style scoped>
.list {
    margin: auto;
    margin-top: 20px;
}
</style>