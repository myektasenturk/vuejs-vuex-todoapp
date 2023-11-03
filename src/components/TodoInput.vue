<template>
    <form class="mb-3" @submit="saveTodo()" @submit.prevent="_default">
        <div class="input-group">
            <input type="text" class="form-control rounded-1 me-3" v-model="selectedTodoValue" required>
            <button class="btn btn-primary rounded-1" type="submit">
                {{ selectedTodoId !== 0 ? 'Güncelle' : 'Ekle' }}
            </button>
        </div>
    </form>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
export default {
    data: () => ({
        selectedTodoId: 0,
        selectedTodoValue: null,
        selectedTodoCompleted: false
    }),

    computed: {
        ...mapGetters([
            'selectedTodo'
        ])
    },

    methods: {
        ...mapActions([
            'newTodo', 'updateTodo', 'selectTodo'
        ]),

        saveTodo() {
            if (this.selectedTodoId === 0) {
                // insert - ekleme
                this.newTodo({
                    value: this.selectedTodoValue,
                    completed: false
                }).then(() => {
                    this.selectedTodoValue = null;
                })
            } else {
                // update - güncelleme
                this.updateTodo({
                    id: this.selectedTodoId,
                    value: this.selectedTodoValue,
                    completed: this.selectedTodoCompleted
                }).then(() => {
                    this.selectTodo(null);
                })
            }
        }
    },

    watch: {
        selectedTodo: function(newValue) {
            this.selectedTodoId = newValue !== null ? newValue.id : 0;
            this.selectedTodoValue = newValue !== null ? newValue.value : null;
            this.selectedTodoCompleted = newValue !== null ? newValue.completed: false;
        }
    }
}
</script>