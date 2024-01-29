<script>
export default {
  name: "App",
  data() {
    return {
      tasks: [
        {
          text: "learn HTML",
          done: true,

        },
        {
          text: "learn JS",
          done: true,

        },
        {
          text: "learn Vue",
          done: false,

        },
      ],
      newTask: "",
      error: false,
    }

  },
  methods: {
    deleteTask(i) {
      this.tasks.splice(i, 1);
    },
    addTask() {
      if (this.newTask != "") {
        const newTaskEl = { text: this.newTask, done: false, };
        let included;
        this.tasks.forEach(task => {
          if (task.text == newTaskEl.text) {
            included = true;
          };
        });
        if (!included) {
          this.error = false;
          this.tasks.push(newTaskEl);
          this.newTask = "";
          console.log(this.tasks);
        } else { this.error = "Your task is already in list" };
      } else { this.error = "You have to type something!" };
    },
    changeDone(i) {
      if (this.tasks[i].done == true) {
        this.tasks[i].done = false;
      } else { this.tasks[i].done = true };
    },
  }
}
</script>

<template>
  <div class="container text-center col-lg-6 my-5">
    <h1 class="text-primary">Todo List</h1>
    <div class="input-group mb-3 ms-auto">
      <input class="form-control" v-model="newTask" @keyup.enter="addTask" type="text" name="newTask" id="newTask"
        placeholder="Insert your new Task">
      <button class="btn btn-outline-primary" @click="addTask">Add</button>
    </div>

    <p class="text-danger" v-if="error">{{ error }}</p>

    <ul class="list-group">
      <li class="list-group-item d-flex" v-for="( task, index ) in  tasks ">
        <input class="form-check-input me-3" type="checkbox" v-model="task.done">
        <div style="width: 100%;" class="d-flex justify-content-between align.items-center">
          <div :class="{ done: task.done }" @click="changeDone(index)">{{ task.text }}</div>
          <div @click="deleteTask(index)"> x</div>
        </div>
      </li>
    </ul>
    <h3 v-if="tasks == ''">You have nothing else to do!</h3>
  </div>
</template>

<style>
/*#region reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
  text-decoration: none;
}

/* #endregion */

.done {
  text-decoration: line-through;
}
</style>
