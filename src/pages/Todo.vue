<template>
  <q-page class="">
    <div class="q-pa-md bg-secondary" >
      <q-input v-model="taskName" dense placeholder="Add" @keyup.enter="addTask" dark>
        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addTask"/>
        </template>
      </q-input>
    </div>
    <q-list separator bordered>
      <q-item
        v-ripple 
        v-for="(item, index) in tasks" 
        :key="item.title" 
        :class="{ 'done text-grey bg-blue-2': item.done }"
        @click="item.done = !item.done"
        clickable
      >
        <q-item-section avatar>
          <q-checkbox v-model="item.done" :val="item.title" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ item.title }}</q-item-label>
        </q-item-section>
        <q-item-section side>
          <q-btn flat round color="primary" icon="delete" @click.stop="removeTask(index)"/>
        </q-item-section>
      </q-item>

    </q-list>
    <div class="absolute-center text-h4 column check" v-show="!tasks.length">
      <q-icon name="check" size="80px" class="col self-center"></q-icon>
      <div class="col">
        No Todo
      </div> 
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      taskName: '',
      tasks: [
        // {
        //   title: 'Get eggs',
        //   done: false
        // },
        // {
        //   title: 'Eat eggs',
        //   done: false
        // }, {
        //   title: 'Poo eggs',
        //   done: false
        // }
      ]
    }
  },
  methods: {
    removeTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Really Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify({
          type: 'positive',
          message: 'delete successful',
          position: 'top'
        })
      })
    },
    addTask () {
      this.tasks.push({
        title: this.taskName,
        done: false
      })
      this.taskName = ''
    }
  }
}
</script>

<style lang="stylus">
  .done
    .q-item__label {
      text-decoration line-through
    }
  .check
    opacity .5
</style>
