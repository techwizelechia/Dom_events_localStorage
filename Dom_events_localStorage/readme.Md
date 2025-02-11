# Intensive Guide: JavaScript DOM Manipulation, Events, and Local Storage

## **1. Understanding the DOM (Document Object Model)**
### **What is the DOM?**
The **Document Object Model (DOM)** is a representation of the structure of an HTML document in JavaScript. It allows JavaScript to manipulate HTML elements dynamically.

### **Accessing DOM Elements**
#### **Methods for Selecting Elements:**
```js
// Selecting by ID
const title = document.getElementById('title');

// Selecting by class
const buttons = document.getElementsByClassName('btn');

// Selecting by tag name
const paragraphs = document.getElementsByTagName('p');

// Modern method (CSS Selectors)
const firstButton = document.querySelector('.btn');
const allButtons = document.querySelectorAll('.btn');
```

#### **Modifying Content & Attributes**
```js
// Changing text content
const heading = document.querySelector('h1');
heading.textContent = 'New Title';

// Changing HTML content
heading.innerHTML = '<span>Styled Title</span>';

// Changing attributes
const link = document.querySelector('a');
link.setAttribute('href', 'https://example.com');
```

### **Creating and Removing Elements**
```js
// Create a new element
const newParagraph = document.createElement('p');
newParagraph.textContent = 'This is a new paragraph.';

document.body.appendChild(newParagraph); // Add to the DOM

// Removing an element
newParagraph.remove();
```

---

## **2. JavaScript Events & Event Listeners**
### **Event Handling Basics**
Events are user interactions like clicks, keypresses, and mouse movements.

#### **Adding Event Listeners**
```js
const button = document.querySelector('#clickMe');
button.addEventListener('click', function() {
    alert('Button Clicked!');
});
```

### **Common Events**
| Event Type | Description |
|------------|-------------|
| `click` | Fired when an element is clicked |
| `mouseover` | Triggered when mouse enters an element |
| `keydown` | When a key is pressed |
| `submit` | When a form is submitted |

#### **Example: Changing Background Color on Click**
```js
const box = document.querySelector('#colorBox');
box.addEventListener('click', () => {
    box.style.backgroundColor = 'blue';
});
```

### **Event Delegation (Handling Multiple Elements Efficiently)**
```js
document.querySelector('#list').addEventListener('click', (e) => {
    if (e.target.tagName === 'LI') {
        alert(`You clicked on: ${e.target.textContent}`);
    }
});
```

---

## **3. Local Storage in JavaScript**
Local Storage is a way to store data in the browser persistently.

### **Storing and Retrieving Data**
```js
// Storing data
localStorage.setItem('username', 'JohnDoe');

// Retrieving data
console.log(localStorage.getItem('username')); // Output: JohnDoe

// Removing data
localStorage.removeItem('username');
```

### **Storing Complex Data (Objects & Arrays)**
```js
const user = { name: 'Alice', age: 25 };
localStorage.setItem('user', JSON.stringify(user));

const retrievedUser = JSON.parse(localStorage.getItem('user'));
console.log(retrievedUser.name); // Output: Alice
```

---

## **4. Hands-on Mini Projects**
### **Project 1: Click Counter (Local Storage + Events)**
```js
const countBtn = document.getElementById('counterBtn');
const display = document.getElementById('counter');
let count = localStorage.getItem('count') ? parseInt(localStorage.getItem('count')) : 0;
display.textContent = count;

countBtn.addEventListener('click', () => {
    count++;
    localStorage.setItem('count', count);
    display.textContent = count;
});
```

### **Project 2: Simple To-Do List (DOM + Events + Local Storage)**
```js
const taskInput = document.getElementById('task');
const addBtn = document.getElementById('addTask');
const taskList = document.getElementById('tasks');

addBtn.addEventListener('click', () => {
    const task = taskInput.value;
    if (task) {
        const li = document.createElement('li');
        li.textContent = task;
        taskList.appendChild(li);

        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        tasks.push(task);
        localStorage.setItem('tasks', JSON.stringify(tasks));
    }
});
```

---

## **5. Intensive Final Project: Task Manager App**
### **Features:**
✅ Add, delete, and mark tasks as complete ✅ Persist data using Local Storage ✅ Event delegation for better performance ✅ Search functionality to filter tasks

```js
document.addEventListener('DOMContentLoaded', () => {
    const taskInput = document.getElementById('taskInput');
    const addTaskBtn = document.getElementById('addTask');
    const taskList = document.getElementById('taskList');

    function loadTasks() {
        taskList.innerHTML = '';
        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        tasks.forEach(task => {
            const li = document.createElement('li');
            li.textContent = task.text;
            if (task.completed) li.style.textDecoration = 'line-through';
            li.addEventListener('click', () => toggleTask(task.text));
            taskList.appendChild(li);
        });
    }

    function toggleTask(taskText) {
        let tasks = JSON.parse(localStorage.getItem('tasks'));
        tasks = tasks.map(task => {
            if (task.text === taskText) task.completed = !task.completed;
            return task;
        });
        localStorage.setItem('tasks', JSON.stringify(tasks));
        loadTasks();
    }

    addTaskBtn.addEventListener('click', () => {
        const taskText = taskInput.value;
        if (taskText) {
            let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
            tasks.push({ text: taskText, completed: false });
            localStorage.setItem('tasks', JSON.stringify(tasks));
            taskInput.value = '';
            loadTasks();
        }
    });

    loadTasks();
});
```

---

## **Tips & Best Practices**
✅ Use **event delegation** for dynamically added elements ✅ Always parse JSON data from Local Storage ✅ Minimize direct DOM manipulations for better performance ✅ Use `console.log()` to debug errors effectively ✅ Write modular functions for reusable code

**Master these, and you’ll be unstoppable in JavaScript! 🚀**

