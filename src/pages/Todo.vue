<template>
  <q-page class="q-pa-lg column">
    <q-list
      separator
      bordered
      
      >
      <q-item
        v-for="(task, index) in tasks"
        :key="task.tittle"
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
          <q-item-label>{{ task.tittle}}</q-item-label>
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
  </q-page>
</template>

<script>
export default {
  data(){
    return {
      tasks: [
        {
          tittle: 'Surasti bananą',
          done: false
        },
        {
          tittle: 'Suvalgyti bananą',
          done: false
        },
        {
          tittle: 'Suvirškinti bananą',
          done: false
        }

      ]
    }
  },
  methods: {
    deleteTask(index, task){
      this.$q.dialog({
        title: 'Confirm',
        message: 'Realy delete task "' + task.tittle + '" ?' ,
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify({
          message: 'Task deleted',
          position: 'center',
          timeout: 500
          })
      })

    }
  },
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
