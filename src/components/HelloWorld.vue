<template>
  <div class="hello">
    <ul>
      <li>
        <input type="checkbox" v-model="newTask.checked" name="newCheckbox" id="newCheckbox" />
        <input
          type="text"
          v-bind:placeholder="placeholderValues.question"
          v-on:keyup.enter="addNewTask"
          v-model="newTask.description"
          name="newTask"
          id="newTask"
        />
        <button id="clearAllBtn" v-on:click="removeAllTasks">Clear List</button>
      </li>
      <li v-for="(item, index) in tasks" v-bind:key="index">
        <input type="checkbox" v-model="item.checked" name="checkbox" id="checkbox" />
        <span>{{item.description}}</span>
        <button id="removeTaskBtn" v-on:click="removeTask(index)">&#10060;</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      tasks: [
        {
          description: "Task 1",
          checked: true
        },
        {
          description: "Task 2",
          checked: false
        }
      ],
      newTask: [
        {
          description: "",
          checked: ""
        }
      ],
      placeholderValues: {
        question: "Insert Tasks Here..."
      }
    };
  },
  methods: {
    addNewTask: function() {
      if (this.newTask.checked) {
        this.newTask.checked = true;
      } else {
        this.newTask.checked = false;
      }

      this.tasks.unshift({
        description: this.newTask.description,
        checked: this.newTask.checked
      });
      (this.newTask.description = ""), (this.newTask.checked = false);
    },
    removeTask: function(taskIndex) {
      this.tasks.splice(taskIndex, 1);
    },
    removeAllTasks: function() {
      this.tasks.splice(0, this.tasks.length);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  border: 1px solid #a5a2a2;
  margin: 15px 60px 0 60px;
  ul {
    overflow: hidden;
    margin: 0px;
    padding: 0;
    li {
      list-style-type: none;
      display: flex;
      justify-content: space-around;
      align-items: center;
      background-color: #3564a4;
      padding: 15px 0;
      margin: 0 0 1px 0;
      &:first-child {
        background-color: #e7e8eb;
        margin: 0px;
        z-index: 1;
        position: relative;
        #newTask {
          border: 1px solid #333;
          width: 65%;
          padding: 15px 10px 15px 10px;
          font-size: 14px;
        }
        #clearAllBtn {
          padding: 12px 20px;
          font-size: 18px;
          color: #333;
          background-color: #fff;
          border: 1px solid #a5a2a2;
        }
      }
      &:last-child {
        margin: 0px;
      }
      #removeTaskBtn {
        margin: 10px 10px 10px 74px;
        background-color: #3564a4;
        border: none;
        font-size: 20px;
        &:hover {
          cursor: pointer;
        }
      }
      #newCheckbox,
      #checkbox {
        width: 20px;
        height: 20px;
      }
      span {
        width: 65%;
        padding: 0 10px;
        font-size: 14px;
        color: #dde2ec;
        text-align: left;
        font-size: 25px;
      }
    }
  }
}
</style>
