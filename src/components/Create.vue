<template>
  <div class="container">
        <div class="card">
            <div class="card-header">
                <h3>Add Alert</h3>
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="addItem">
                    <div class="form-group">
                        <label>Keyword to monitor:</label>
                        <input type="text" class="form-control" v-model="item.phrase"/>
                    </div>

                    <div class="form-group">
                        <input type="submit" class="btn btn-primary" value="Add Item"/>
                    </div>
                </form>
            </div>
        </div>
        <div class="card mt-3" v-if="isSubmitted">
            <div class="card-body">
                <h4 class="card-title">Alert created successfully!</h4>
                <p>Phrase: <b>{{ submittedItem.phrase }}</b></p>
                
            </div>
        </div>
    </div>
</template>

<script>
export default {
  components: {
      //name: 'AddItem'
  },
  data() {
      return {
          item: {},
          isSubmitted: false,
          submittedItem: {},
      }
  },
  methods: {
      addItem() {
           let uri = 'http://localhost:3000/dev/item';
            this.axios.post(uri, this.item).then((response) => {
                console.log(response.data)
                
            });
            this.isSubmitted = true;
            this.submittedItem = {...this.item}
            this.item.phrase = '';
        }
    }
}
</script>