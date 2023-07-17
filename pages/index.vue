<template>
  <div class="row todo-content">
    <div class="col-md-6">
      <div class="todo-list not-done">
        <h1>TODO LIST</h1>
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="Enter task" v-model="taskContent">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" type="button" id="button-addon2" @click="addTasks()">Add</button>
          </div>
        </div>
        <hr>
        <ul class="list-unstyled" v-for="(todo, index) in todos" :key="todo.id">
          <li class="ui-state-default li-items mt-1">
            <div class="input-group">
              <div class="input-group-prepend">
                <div class="input-group-text h-full">
                  <input class="cursor-pointer" type="checkbox" aria-label="Radio button for following text input" v-model="todo.checked">
                </div>
              </div>
              <input type="text" :class="['form-control', {'done-task': todo.completed}]" v-model="todo.content">
              <div class="input-group-append remove-icon">
                <span class="input-group-text" @click="delTasks(index)">&#10060;</span>
              </div>
            </div>
          </li>
        </ul>
        <hr>
        <div class="todo-footer row">
          <div class="col-md-6">
            <div class="form-check form-check-inline" @click="checkAll(true)">
              &#9989;
              <label class="form-check-label" for="inlineRadio1">Check all</label>
            </div>
            <div class="form-check form-check-inline" @click="checkAll(false)">
              &#10062;
              <label class="form-check-label" for="inlineRadio2">UnCheck all</label>
            </div>
          </div>
          <div class="col-md-6 save-all">
            <div class="form-check form-check-inline save-all">
              <button type="button" class="btn btn-success btn-sm" @click="doneAll()">DONE ALL &#10004;</button>
            </div>
            <div class="form-check form-check-inline save-all">
              <button type="button" class="btn btn-dark btn-sm" @click="deleteAll()">DELETE ALL &#10006;</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap-vue/dist/bootstrap-vue.css';

export default {
  name: 'Index',

  data () {
    return {
      todos: [
        {
          'id': 1,
          'content': 'Viec can lam 1',
          'checked': false,
          'completed': false,
        },
        {
          'id': 2,
          'content': 'Viec can lam 2',
          'checked': false,
          'completed': false,
        }
      ],
      taskContent: '',
      code: 2,
    }
  },
  methods: {
    addTasks() {
      if(this.taskContent.trim().length === 0) {
        this.taskContent = '';
      }
      this.code++;
      this.todos.push (
        {
          'id': this.code,
          'content': this.taskContent,
          'checked': false,
          'completed': false,
        }
      )
      this.taskContent = '';
    },

    delTasks(index) {
      this.todos.splice(index, 1);
    },

    checkAll(flag) {
      this.todos.forEach(todo => {
        todo.checked = flag;
      })
    },

    doneAll() {
      this.todos.filter((item) => {
        if(item.checked) {
          item.completed = true;
        }
      });
      this.checkAll(false);
    },

    deleteAll() {
      this.todos = this.todos.filter((item) => {
        return !item.checked;
      });
    }
  },

  // created () {
  //   console.log(this.todos);;
  // },
}
</script>
<style scoped>
.todo-content {
  display: flex;
  justify-content: center;
}

.todo-list h1 {
  margin-top: 20px;
  padding-bottom: 20px;
  text-align: center;
  font-weight: bold;
}

.todo-footer {
  background-color: #d2e8ca;
  padding: 10px 20px 15px;
}

#done-items li {
  padding: 10px 0;
  border-bottom: 1px solid #ddd;
  text-decoration: line-through;
}

.done-task {
  text-decoration: line-through;
  color: #61BB27;
}

.form-check-inline {
  cursor: pointer;
}

.remove-icon span {
  cursor: pointer;
}

.save-all {
  float: right;
}
</style>
