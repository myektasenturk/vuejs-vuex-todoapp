<template>
    <ul class="list-group border-0">
        <li class="list-group-item border-0 my-1 d-flex justify-content-between align-items-center bg-body-secondary"
            v-for="item, key in todoList" :key="key">
            <div class="form-check">
                <input class="form-check-input" type="checkbox" @click="completeTodo(item)">
                <label class="form-check-label" :class="item.completed ? 'text-decoration-line-through' : ''" for="flexCheckDefault">
                    {{ item.value }}
                </label>
            </div>

            <div class="d-flex align-items-center">
                <button class="btn border-0 text-secondary" @click="selectTodo(item)">
                    <i class="bi bi-pencil-square fs-5"></i>
                </button>

                <button class="btn border-0 text-danger" @click="removeTodo(item.id)">
                    <i class="bi bi-trash2-fill fs-5"></i>
                </button>
            </div>
        </li>
    </ul>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
    computed: {
        ...mapGetters([
            'todoList'
        ])
    },

    methods: {
        ...mapActions([
            'selectTodo', 'deleteTodo', 'updateTodo'
        ]),

        removeTodo(id) {
            const confirmBox = confirm('Silinecektir. Emin misiniz?');

            if (confirmBox) {
                this.deleteTodo(id).then(() => this.selectTodo(null));
            }
        },

        completeTodo(todo) {
            todo.completed = !todo.completed;
            this.updateTodo(todo);
        }
    }
}
</script>