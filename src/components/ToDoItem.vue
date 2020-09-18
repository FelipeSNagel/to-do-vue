<template>
  <li class="tile" :class="{checked: toDo.checked}">
    <div class="tile-icon">
      <i class="icon centered" :class="toDo.checked ? 'icon-check' : 'icon-time'"></i>
    </div>

    <div class="tile-content">
      <p class="title-subtitle">{{ toDo.description }}</p>
    </div>

    <div class="title-action">
      <button @click="$emit('toggle', toDo)" class="btn btn-link">
        <span v-if="toDo.checked">Desmarcar</span>
        <span v-else>Concluído</span>
      </button>
      <button @click="$emit('remove', toDo)" class="btn btn-link text-error">Remover</button>
    </div>
  </li>
</template>

<script>

export default {
  props: {
    toDo: { type: Object, required: true },
  },
};

</script>

<style scoped>
  .checked {
    text-decoration: line-through;
    color: lightgray;
  }
</style>
