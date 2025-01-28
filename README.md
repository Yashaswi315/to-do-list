<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f4f4f9;
        }

        .todo-app {
            width: 90%;
            max-width: 500px;
            background: #ffffff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .todo-app h1 {
            text-align: center;
            font-size: 24px;
            color: #333;
            margin-bottom: 20px;
        }

        .input-section {
            display: flex;
            gap: 10px;
        }

        .input-section input {
            flex: 1;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }

        .input-section button {
            padding: 10px;
            font-size: 16px;
            color: #fff;
            background-color: #28a745;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .input-section button:hover {
            background-color: #218838;
        }

        .task-list {
            margin-top: 20px;
        }

        .task-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
            background-color: #fff;
        }

        .task-item input {
            flex: 1;
            margin-right: 10px;
            border: none;
            background: none;
            font-size: 16px;
        }

        .task-item input:disabled {
            color: #333;
        }

        .task-item button {
            margin-left: 5px;
            padding: 5px 10px;
            font-size: 14px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .edit-btn {
            background-color: #ffc107;
            color: #fff;
        }

        .edit-btn:hover {
            background-color: #e0a800;
        }

        .delete-btn {
            background-color: #dc3545;
            color: #fff;
        }

        .delete-btn:hover {
            background-color: #c82333;
        }
    </style>
</head>
<body>
    <div class="todo-app">
        <h1>To-Do List</h1>
        <div class="input-section">
            <input type="text" id="new-task" placeholder="Enter a new task">
            <button id="add-task">Add</button>
        </div>
        <div class="task-list" id="task-list"></div>
    </div>

    <script>
        const newTaskInput = document.getElementById('new-task');
        const addTaskButton = document.getElementById('add-task');
        const taskList = document.getElementById('task-list');

        function createTaskElement(taskText) {
            const taskItem = document.createElement('div');
            taskItem.className = 'task-item';

            const taskInput = document.createElement('input');
            taskInput.type = 'text';
            taskInput.value = taskText;
            taskInput.disabled = true;

            const editButton = document.createElement('button');
            editButton.className = 'edit-btn';
            editButton.textContent = 'Edit';

            const deleteButton = document.createElement('button');
            deleteButton.className = 'delete-btn';
            deleteButton.textContent = 'Delete';

            editButton.addEventListener('click', () => {
    if (taskInput.disabled) {
        taskInput.disabled = false;
        editButton.textContent = 'Save';
    } else {
        taskInput.disabled = true;
        editButton.textContent = 'Edit';
    }
});


            deleteButton.addEventListener('click', () => {
                taskList.removeChild(taskItem);
            });

            taskItem.appendChild(taskInput);
            taskItem.appendChild(editButton);
            taskItem.appendChild(deleteButton);

            return taskItem;
        }

        addTaskButton.addEventListener('click', () => {
            const taskText = newTaskInput.value.trim();
            if (taskText) {
                const taskElement = createTaskElement(taskText);
                taskList.appendChild(taskElement);
                newTaskInput.value = '';
            }
        });

        newTaskInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                addTaskButton.click();
            }
        });
    </script>
</body>
</html>
