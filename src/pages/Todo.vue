<template>
  <q-page class="q-pa-lg column">
    <div class="row q-pa-sm bg-primary">

      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        square
        filled
        bg-color="white"
        placeholder="Add task"
        dense
        ref="addTaskBar"
        >
        <template v-slot:append>
          <q-btn
            @click="addTask"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>

    </div>
    <q-list
      separator
      bordered
      
      >
      <q-item
        v-for="(task, index) in tasks"
        :key="task.title"
        v-ripple
        clickable
        @click="task.done = !task.done"
        :class="{'done bg-blue-1' : task.done}"
        >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            val="teal"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side
        >
         <q-btn
            @click.stop="deleteTask(index, task)"
            flat
            round
            dense
            color="primary"
            icon="delete" />
        </q-item-section>
      </q-item>

      
    </q-list>
    <div
      v-if="!tasks.length"
      class="no-tasks absolute-center"
      style="opacity: 0.5">
      <q-icon 
        name="check"
        size="100px"
        color="primary"
      />
      <div class="text-h5 text-primary text-center">
        No tasks
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data(){
    return {
      newTask: '',
      tasks: [
        {
          title: 'Surasti bananą',
          done: false
        },
        {
          title: 'Suvalgyti bananą',
          done: false
        },
        {
          title: 'Suvirškinti bananą',
          done: false
        }

      ]
    }
  },
  methods: {
    deleteTask(index, task){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Realy delete task "' + task.title + '" ?' ,
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify({
          message: 'Task deleted',
          type: 'info',
          position: 'top',
          timeout: 1000
          })
      })

    },
    addTask(){
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  },
  mounted(){
    this.$refs.addTaskBar.$el.focus() //focus cursor in input field on page load
  }
}
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }
</style>
