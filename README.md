V3 Requirements:

It should store the todos array on an object //
It should have a displayTodos method //
It should have an addTodos method //
It should have a changeTodo method //
It should have a deleteTodo method //

V4 Requirements:

todoList.addTodo should add objects //
todoList.changeTodo should change the todoText property //
todoList.toggleCompleted should change the completed property //

V5 Requirements:
.displayTodos should show .todoText
.displayTodos should tell you if .todos is empty
.displayTodos should show .completed

V6 Requirements:
.toggleAll : If everything's true, making everything false
.toggleAll : Otherwise, make everything true.

V7 Requirements:
There should be a "Display Todos" button and a "Toggle all" button in the app.
Clicking "Display todos" should run todoList.displayTodos.
Clicking "Toggle all" should run todoList.toggleAll.

V8 Reqiurements:
It should hve working ontrols for .addTodo
It should hav working controls for .changeTodo
It should have working controls for .deleteTodo
It should have workings controls for .toggleCompleted

V9
There should be an li element for every to
Each li element should contain .todoText
Each li element should show .completed

V10
There should be a way to create delete buttons
There should be a delete button for each todo
Each li should have an id that has the todo position
Delete buttons should have access to the todo id
Clicking delete should update todoList.todos and the DOM


My old code - still works! But with comments

//this keyword refers to entire object ; can be used to-reference methods in the object
//object and method functions are -- todoList.displayTodos, todoList.addTodo, 
//todoList.changeTodo, todoList.deleteTodo, todoList.toggleAll
//make sure to add commas to add additional method

var todoList = {  //model
  
  //objects: think of switch case style.  Commas are substituted for breaks.
  //convention is methodName: function() {}, or arrayName: [],
  
  todos: [],       // empty array to fill
  //make sure to add commas to add additional method
  
  addTodo: function(todoText) {  //addTodo method, takes in one param., and uses .push next item in array to end of list
    this.todos.push({           //pushes objects to array
      todoText: todoText,     
      completed: false        //completed property, true or false boolean
    });
      //displays current list of todos after main method
    
  }, //END OF .addTodo method
  
  changeTodo: function(position, todoText) {   //takes in two variables, position of to-be-changed and the changed text
    this.todos[position].todoText = todoText;     //uses . notation to grab todoText property and set it to new value when function is run
                  //displays current list of todos after main method
  }, //END OF .changeTodo method
  
  deleteTodo: function(position) {       //delete method that takes in one param
    this.todos.splice(position, 1);     //uses .splice to find array position like 0, and to only delete one item in array
                 //displays current list of todos after main method
  }, //END OF .deleteTodo method
  
  toggleCompleted: function(position){
    var todo = this.todos[position];    //grabbing and saving reference in specific todo we're interested in
    todo.completed = !todo.completed;    //bang operator - if false, will switch to true.  If true, switches to false
    
  },  //END OF .toggleCompleted method
  
  toggleAll: function() {              //toggleAll method that that creates two variables and uses nested for/if statements
    var totalTodos = this.todos.length;  //variable to grab total length of todos added
    var completedTodos = 0;              //variable counter to tally completed todos
    
    //Get number of completed todos
    for (var i = 0; i < totalTodos; i++)  // for/if statement
    {
      if(this.todos[i].completed === true){
        completedTodos++;
      }
    }
    //Case 1 : .toggleAll : If everything's true, making everything false
    if (completedTodos === totalTodos)     // if/for statement
    {
      //Make everything false
      for (var i = 0; i < totalTodos; i++) {
        this.todos[i].completed = false;
      }
    // Case 2: Otherwise, make everything true
    } 
    else //Make everything true         // else/for statement
    { 
      for (var i = 0; i < totalTodos; i++) {
        this.todos[i].completed = true;
      }
    }
  }   //END OF .toggleAll method
};


var handlers = {  //controller
  addTodo: function() {
    var addTodoTextInput = document.getElementById('addTodoTextInput');
    todoList.addTodo(addTodoTextInput.value);
    addTodoTextInput.value = ''; // will clear input text after inputting
    view.displayTodos();
  },
  
  changeTodo: function() {
    var changeTodoPositionInput = document.getElementById('changeTodoPositionInput');
    var changeTodoTextInput = document.getElementById('changeTodoTextInput');
    todoList.changeTodo(changeTodoPositionInput.valueAsNumber, changeTodoTextInput.value);
    changeTodoPositionInput.value ='';
    changeTodoTextInput.value = '';
    view.displayTodos();
  },
  
  deleteTodo: function() {
    var deleteTodoPositionInput = document.getElementById('deleteTodoPositionInput');
    todoList.deleteTodo(deleteTodoPositionInput.valueAsNumber);
    deleteTodoPositionInput.value = '';
    view.displayTodos();
  },
  
  toggleCompleted: function() {
    var toggleCompletedPositionInput = document.getElementById('toggleCompletedPositionInput');
    todoList.toggleCompleted(toggleCompletedPositionInput.valueAsNumber);
    toggleCompletedPositionInput.value = '';
    view.displayTodos();
    
  },
   toggleAll: function() {
    todoList.toggleAll();
    view.displayTodos();
  }
};

var view = {   //view; responsible for taking todos array and displaying onto screen
  
  displayTodos: function() {
      var todosUl = document.querySelector('ul'); //grabs ul html
      todosUl.innerHTML = '';  //clears ul and starts from 0
      for (var i = 0; i < todoList.todos.length;i++) {  //creates list item for each item in todos array
        var todoLi = document.createElement('li');  //creates new li element
        var todo = todoList.todos[i];
        var todoTextWithCompletion = '';
        
        if (todo.completed === true) {
          todoTextWithCompletion = '(x) ' + todo.todoText;
        } else {
           todoTextWithCompletion = '( ) ' + todo.todoText;
        }
        
        todoLi.textContent = todoTextWithCompletion;   //access and sets text content of element in markup
        todosUl.appendChild(todoLi);    //add it to ul element
    }
  }
};


/* Older simpler code like above but without refactoring w/ html below and the js below that


    <button id="displayTodosButton">Display Todos</button>
    <button id="toggleAllButton">Toggle All</button>
    

// 1. We want to get access to the display todos button
var displayTodosButton = document.getElementById('displayTodosButton');
var toggleAllButton = document.getElementById('toggleAllButton');

// 2. We want to run displayTodos and toggleAll methods, when someone clicks the display/toggle all
// todos button by adding an event listener, which will run this function

displayTodosButton.addEventListener('click', function(){
  todoList.displayTodos();
});

toggleAllButton.addEventListener('click', function() {
  todoList.toggleAll();
});

*/




