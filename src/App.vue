<template>
  <div class=" position-absolute top-50 start-50 translate-middle w-50">
    <div class="card">
      <div class="card-header py-3">
        <h2 class="card-title mb-0">
          Yapılacaklar listesi
        </h2>
      </div>
      <div class="card-body">
        <TodoInput />

        <TodoList />
      </div>
    </div>
  </div>
</template>

<script>
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';

export default {
  components: {
    TodoInput,
    TodoList
  }
}
</script>