<script>
import {defineComponent} from 'vue'
import TabContent from "./components/TabContent.vue";
import Tab from "./components/Tab.vue";
import TasksList from "./components/TasksList.vue";
import task from "./components/Task.vue";

export default defineComponent({
  name: "App",
  components: {TasksList, Tab, TabContent},
  data() {
    return {
      activeTab: 0,
      newTask: '',
      tasks: [
        { id: 1, text: 'Hello world!', completed: false },
        { id: 2, text: 'Completed', completed: true }
      ]
    };
  },
  computed: {
    activeTasks() {
      return this.tasks.filter(task => task.completed === false);
    },
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    }
  },
  methods: {
    activateTab(number) {
      this.activeTab = number;
    },
    appendTask() {
      this.tasks.push({ id: this.tasks.length + 1, text: this.newTask, completed: false });
      this.newTask = '';
    },
    updateStatus(id, status) {
      const element = this.tasks.find(task => task.id === id);
      const index = this.tasks.indexOf(element);
      element.completed = status;
      this.tasks[index] = element;
    }
  }
})
</script>

<template>
  <section class="vh-100 gradient-custom">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-xl-10">

          <div class="card">
            <div class="card-body p-5">

              <form class="d-flex justify-content-center align-items-center mb-4" @submit="appendTask">
                <div class="form-outline flex-fill">
                  <input type="text" id="form2" class="form-control" v-model="newTask" />
                  <label class="form-label" for="form2">New task...</label>
                </div>
                <button type="submit" class="btn btn-info ms-2">Add</button>
              </form>

              <!-- Tabs navs -->
              <ul class="nav nav-tabs mb-4 pb-0" id="ex1" role="tablist">
                <Tab target="ex1-tabs-1" label="All" @activate="activateTab(0)" :is-active="activeTab === 0"></Tab>
                <Tab target="ex1-tabs-2" label="Active" @activate="activateTab(1)" :is-active="activeTab === 1"></Tab>
                <Tab target="ex1-tabs-3" label="Completed" @activate="activateTab(2)" :is-active="activeTab === 2"></Tab>
              </ul>
              <!-- Tabs navs -->

              <!-- Tabs content -->
              <div class="tab-content" id="ex1-content">
                <TabContent v-if="activeTab === 0">
                  <TasksList :tasks="tasks" @update-status="updateStatus"></TasksList>
                </TabContent>
                <TabContent v-if="activeTab === 1">
                  <TasksList :tasks="activeTasks" @update-status="updateStatus"></TasksList>
                </TabContent>
                <TabContent v-if="activeTab === 2">
                  <TasksList :tasks="completedTasks" @update-status="updateStatus"></TasksList>
                </TabContent>
              </div>
              <!-- Tabs content -->
            </div>
          </div>

        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>