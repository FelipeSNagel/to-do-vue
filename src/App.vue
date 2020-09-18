<template>
  <div id="app">
    <div class="container grid-xs py-2">
      <h1 class="title flex-centered">To-<span>Do</span> List <i class="icon icon-check"></i></h1>

      <form @submit.prevent="addToDo(toDo)">
        <div class="input-group">
          <input v-model="toDo.description" type="text" class="form-input" placeholder="Novo toDo"/>
          <button class="btn btn-primary input-group-btn">Adicionar</button>
        </div>
      </form>
      <ul class="todo-list">
        <ToDoItem v-for="t in toDos" :key="t.id" :toDo="t"
          @toggle="toggleToDo" @remove="removeToDo"
         />
      </ul>
    </div>
  </div>
</template>

<script>

import ToDoItem from './components/ToDoItem.vue';

export default {
  name: 'App',
  components: {
    ToDoItem,
  },
  data() {
    return {
      toDos: [],
      toDo: {
        checked: false,
      },
    };
  },
  methods: {
    addToDo(toDo) {
      this.toDos.push({
        ...toDo,
        id: Date.now(),
      });

      this.toDo = { checked: false };
    },

    toggleToDo(param) {
      const index = this.toDos.findIndex((item) => item.id === param.id);

      if (index > -1) {
        const checked = !this.toDos[index].checked;
        this.$set(this.toDos, index, { ...this.toDos[index], checked });
      }
    },

    removeToDo(param) {
      const index = this.toDos.findIndex((item) => item.id === param.id);

      if (index > -1) {
        this.$delete(this.toDos, index);
      }
    },

  },

};
</script>

<style scoped>
  .title {
    font-size: 25px;
    font-weight: 700;
    color: #3b3b3b;
    margin: 30px auto;
  }

  .title span {
    color: #5755d9;
  }

  .title i {
    color: #5755d9;
    margin-left: 0.5rem;
  }

  .todo-list {
    padding-top: 2rem;
  }
</style>
