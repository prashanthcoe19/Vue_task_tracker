<template>
    <div
        @dblclick="$emit('toggle-reminder', task.id)"
        :class="[task.reminder ? 'reminder' : '', 'task']"
    >
        <h3>
            {{ task.text }}
            <p>
                <i
                    @click="$emit('delete-task', task.id)"
                    class="fas fa-times"
                ></i>
                <i @click="toggleEditTask" class="fas fa-edit"></i>
            </p>
        </h3>
        <p>{{ task.day }}</p>
    </div>
    <EditTask
        v-show="showEditTask"
        :text="task.text"
        :day="task.day"
        :reminder="task.reminder"
        :id="task.id"
        @edit-task="editTask"
    />
</template>

<script>
import EditTask from './EditTask.vue';
export default {
    name: 'Task',
    props: {
        task: Object
    },
    components: {
        EditTask
    },
    data() {
        return {
            showEditTask: false
        };
    },
    methods: {
        toggleEditTask() {
            this.showEditTask = !this.showEditTask;
        },
        editTask(task) {
            this.$parent.$emit('edit-task', task);
        }
    },
    emits: ['edit-task']
};
</script>

<style scope>
.fas {
    color: red;
}
.task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}
.task.reminder {
    border-left: 5px solid green;
}
.task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>
