<template>

  <div class="container">
    <input type = "text" class="todo-input" placeholder="What needs to be done ?"
    v-model = 'newTodo' @keyup.enter = "addTodo">
    <!--Here we used v-model that will make our "two way data binding" 
    whatever we put in input will be stored in our variable "newTodo"-->
    <!--the keyup is an eventlistener that will call
    our function that add the task when the user press enter-->
    
    <div class= "todo-item"
    v-for= "(task, index) in testTasks" :key= "task.id" >
    <!--Here we created a for loop to run over the array-->
    <!--And We set the task and the index as the counter/parameters-->
      
      <!--div for tasks--->
      <div class="todo-item-left">
        <input type="checkbox" v-model="task.completed">
        <!--The if will show the label if we are not editing-->
        <!-- we have to use our counter "task" as parameter, not the array name-->
        
        <div class="todo-item-label"
         v-if="!task.editing" @dblclick="editTodo(task)"
        :class="{  completed : task.completed}">
          {{ task.title }}
        </div>
        <!--The edit function will be called with a double click
        :class="{  completed : todo.completed}: this was a if
        with v-bind to apply a css if the conditional is right -->

        <!--Using v-model for two way data binding to edit task-->
        <input v-else class="todo-item-edit" type="text" v-model="task.title"
        @blur="doneEdit(task)"  @keyup.enter="doneEdit(task)" @keyup.esc="cancelEdit(task)" v-focus>
         <!--And the else will turn the field edit on-->
         <!---we add the blur and keyup, to finish edit when its over, calling the function for it-->
         <!---Our custom directive v-focus, to use the blur properly-->
      </div>
    
      <!--div to remove task--->
      <div class="remove-item" @click="removeTodo(index)">
      <!--When the remove icon be clicked, it will call this function-->
        &times;
      </div>
    </div>
    <div class="status-container">
      <div><label><input type="checkbox">Check All</label></div>
      <div>{{ remaining }} items left </div>
    </div>
  </div>  
</template>

<script>
export default {
  name: 'toDo',
  data () {
    return{
    //here is the variable that will get the tasks
      newTodo: '',
      taskId: 3,
      beforeEdited: '',
      
      //here we are creating an array to have some previous tasks 
      testTasks: [
        //an array of objects 
        {
          'id': 1,
          'title': 'study vue',
          'done': false,
          //we´ll use this status as a conditional
          //in the edit funtion
          'editing': false,
        },
        {
          'id': 2,
          'title': 'do the homework',
          'done': false,
          'editing': false,
        },
      ]

    }
  },
  //here is how we used a custom directive
  directives: {
    focus: {
      inserted: function (el) {
        //when we are using it to focus
        //for using better our @blur
        el.focus ()
      }
    }
  },
  
  methods: {

    //this method will add the inputs in the task array
    addTodo () {
      //a conditional to not let blank inputs 
      if (this.newTodo.trim().length == 0) {
        // we made it with the trim and length methods
        return
      }
     //using the method that will actually do this
      this.testTasks.push ( {
        //referencing the id that is in the array 
        id: this.taskId,
        //referencing the variable that will store the inputs
        title: this.newTodo,
        //setting task status as false by default,
        //to turn on in the function
        completed: false,
        editing: false
        
      })
      //setting the variable to receive the tasks 
      this.newTodo = '';
      //setting the id variable to grow as the tasks are coming
      this.taskId++
    },

    //our function to edit tasks
    editTodo (task) {
      //we did it only changing the status that we set in our array
      //with that it will be caugth in the if condiitonal
      //opening the text field
      this.beforeEdited = task.title;
      //and we set the title as this,
      //to use in the cancel edit function
      task.editing = true;
      
    },
    
    //this is for finish the edit
    doneEdit (task) {
       //a conditional to not let blank inputs 
      if (task.title.trim().length == 0) {
        // we made it with the trim and length methods
        task.title = this.beforeEdited
        //if its blank space, it will become how it was be4
      }
      //we did it only setting to the initial state
      task.editing = false;
    },

    //similar to done edit, but its called when pressed esc
    //and the title will be how it was, cuz was not changed
    cancelEdit (task) {
      task.title = this.beforeEdited
      task.editing = false;
    },

    //here is the func that will delete the tasks
    removeTodo (index) {
      //actually is very simple, we just used the method "splice"
      this.testTasks.splice(index, 1)
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.container {
  max-width: 600px;
  margin: 0 auto;
}

.container{
  margin-top: 1px;
}

.todo-input{
  width: 100%;
  padding: 10px 18px;
  font-size: 18px;
  margin-bottom: 16px;
  outline: 10px;
}

.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.remove-item:hover {
  cursor: pointer;
  margin-left: 14px;
  color: red;
}

.todo-item-left {
  display: flex;
  align-items: center;
}

.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;
}

.todo-item-edit {
  font-size: 20px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

.todo-item-edit:focus {
  outline: none;
}

.completed {
  text-decoration: line-through;
  color: red;
}

.status-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  border-top: 1px solid lightgrey;
  padding-top: 14px;
  margin-bottom: 14px;
}

.status-container button {
  font-size: 14px;
  background-color:white ;
  appearance: none;
}

.status-container button:hover{
  background: lightgreen;
  
}

.status-container button:focus {
  outline: none;
}

.active{
  background: lightgreen;
}



</style>
  
  

