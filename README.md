
# Wishlist

Wishlit is a super cool to add your bucket list, and have stored for a life time.


## Tech Stack

- HTML/CSS
- Javascript


## Author

-   Prakash Sakari - follow me on 👇
-   [GitHub](https://www.github.com/prakashsakari)
-   [LinkedIn](https://www.linkedin.com/in/prakashsakari/)
-   [Twitter](https://twitter.com/prakashsakari)


## Live Link

https://makewishlist.netlify.app/


## Run Locally

Clone the project by adding the following command in the terminal.
Make sure your have git installed and added to path.

```bash
  git clone https://github.com/prakashsakari/wishlist.git
```

Open the project directory in a new window and run the html file

function uuid() {
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
        var r = Math.random() * 16 | 0,
            v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}

let todoInput = document.querySelector(".input");
let addTodoButton = document.querySelector(".button");
let showTodos = document.querySelector(".todos-container");
let todo = "";

let localData = JSON.parse(localStorage.getItem("todos"));
let todoList = localData || [];

addTodoButton.addEventListener("click", (e) => {
    e.preventDefault();
    todo = todoInput.value;
    if (todo.length > 0) {
        todoList.push({
            todo,
            id: uuid(),
            isCompleted: false
        });
        renderTodoList(todoList);
        localStorage.setItem("todos", JSON.stringify(todoList));
        todoInput.value = "";
    }
});

showTodos.addEventListener("click", (e) => {
    e.preventDefault();
    let key = e.target.dataset.key;
    let delTodoKey = e.target.dataset.todokey;
    todoList = todoList.map((todo) =>
        todo.id === key ? {
            ...todo,
            isCompleted: !todo.isCompleted
        } : todo
    );
    todoList = todoList.filter((todo) => todo.id !== delTodoKey);
    localStorage.setItem("todos", JSON.stringify(todoList));
    console.log(todoList);
    renderTodoList(todoList);
});

function renderTodoList(todoList) {
    showTodos.innerHTML = todoList.map(
        ({
            todo,
            id,
            isCompleted
        }) =>
        `<div class="todo relative"> <input id="item-${id}" data-key=${id} class="t-checkbox t-pointer" type="checkbox" ${
        isCompleted ? "checked" : ""
      }> <label data-key=${id} class="todo-text t-pointer ${
        isCompleted ? "checked-todo" : ""
      }" for="item-${id}"> ${todo} </label> <button class="absolute right-0 button cursor">
      <span data-todokey=${id}  class="del-btn material-icons-outlined">delete</span>
            </button> </div>`
    );
}

renderTodoList(todoList);