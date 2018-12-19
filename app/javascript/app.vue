<template>
  <div id="app" class= "row">
    <div v-for="(list, index) in lists" class = "col-3">
        <h6>{{ list.name }}</h6>
        <hr />
        <div v-for="(card, index) in list.cards" class="card card-body mb-3">
            {{ card.name }}
        </div>
        <div class="card card-body">
            <textarea class="form-control" v-model="messages[list.id]"></textarea>
            <button v-on:click="submitMessages(list.id)" class="btn btn-secondary">Add</button>
        </div>
    </div>
  </div>
</template>

<script>
import Rails from 'rails-ujs'
Rails.start()

export default {
    props: ["original_lists"],
    data: function(){
        return {
            messages: {},
            lists: this.original_lists,
        }
    },
    methods:{
        submitMessages: function(list_id){
            this.messages[list_id]
            var data = new FormData
            data.append("card[list_id]", list_id)
            data.append("card[name]", this.messages[list_id])
            console.log('afsafas');
            Rails.ajax({
                url: "/cards",
                type: "POST",
                data: data,
                dataType: "json",
                success: (data) => {
                    const index = this.lists.findIndex(item => item.id == list_id)
                    this.lists[index].cards.push(data)
                    this.messages[list_id] = undefined
                }
            });
        }
    }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
