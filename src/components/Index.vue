<template>
    <div>
        <h1>Alerts</h1>

        <table class="table table-hover">
            <thead>
            <tr>
                <td>Keyword</td>
                <td>Last scanned</td>
                <td>Actions</td>
                <td></td>
            </tr>
            </thead>

            <tbody>
                <tr v-for="item in items" :key="item._id">
                    <td>{{ item.phrase }}</td>
                    <td>{{ new Date(item.last_scanned).toISOString() }}</td>
                    <td><router-link :to="{name: 'Edit', params: { id: item._id }}" class="btn btn-primary">Edit</router-link></td>
                    <td><button class="btn btn-danger"  v-on:click="deleteItem(item._id)">Delete</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

    export default {
        data(){
            return{
                items: []
            }
        },

        created: function()
        {
            this.fetchItems();
        },

        methods: {
            fetchItems()
            {
              let uri = 'http://localhost:3000/dev/item';
              this.axios.get(uri).then((response) => {
                  this.items = response.data["response_items"];
              });
            },
            deleteItem(id)
            {
              let uri = 'http://localhost:3000/dev/item/'+id;
              console.log(uri)
              this.items.splice(id, 1);
              this.axios.delete(uri);
            }
        }
    }
</script>