<template>
  <div class="todos">
    <h1>Todo List <button @click="showAddForm = true;" type="button">+ Add</button></h1>
    <div>
      <form v-if="showAddForm" v-on:submit="add" action="#">
        <label>Add new item to the list:</label>
        <input
          v-model="newTodoText"
          type="text" placeholder="Do something"/>

        <button type="submit">+ Add</button>
        <button @click="showAddForm = false;" type="button">Cancel</button>
      </form>

      <hr>

      <p>Pending: <span>{{countResolved}}</span></p>
      <ul class="items">
        <li v-for="item, index in items">
          <label title="Resolve" :class="item.resolved ? 'resolved' : ''">
            <input v-model="item.resolved" type="checkbox" name="resolved" :checked="item.resolved"> {{item.text}}
          </label>
          <a title="Remove" @click="remove($event, index)" href="#">X</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Todos',

    data: function () {
      return {
        newTodoText: '',
        items: [],
        unresolvedCount: 0,
        showAddForm: false
      }
    },

    methods: {
      add: function (e) {
        e.preventDefault();

        this.items.push({
          text: this.newTodoText,
          resolved: false
        });

        this.newTodoText = '';
        this.showAddForm = false;
      },

      remove: function (e, index) {
        e.preventDefault();

        this.items.splice(index, 1)
      }
    },

    computed: {
      countResolved: function () {
        return this.items.filter((item) => {
          return !item.resolved;
        }).length
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  a {
    color: #42b983;
  }

  .items {
    list-style-type: none;
    padding: 0;
  }

  .items > li {
    display: block;
    list-style: none;
  }
  .resolved {
    text-decoration: line-through;
  }
</style>
