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
  }
}
</script>

<template>
  <div class="text-center">
    <h1>Todo List</h1>

    <input v-model="newTask" @keyup.enter="addTask" type="text" name="newTask" id="newTask"
      placeholder="Insert your new Task">
    <button @click="addTask">Add</button>

    <p class="text-danger" v-if="error">{{ error }}</p>

    <ul>
      <li v-for="( task, index ) in  tasks ">
        <span :class="{ done: task.done }">{{ task.text }}</span>
        <span @click="deleteTask(index)"> x</span>
      </li>
    </ul>
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
