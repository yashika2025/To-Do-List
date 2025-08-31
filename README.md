<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Cute To-Do App</title>
    <!-- Bootstrap CDN -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            background: linear-gradient(135deg, #ffe6f0, #fff0f5);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            max-width: 450px;
            width: 100%;
            background-color: #fff0f5;
            padding: 30px 25px;
            border-radius: 20px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
        }
        h2 {
            text-align: center;
            color: #ff69b4;
            margin-bottom: 15px;
        }
        p {
            text-align: center;
            font-size: 0.9rem;
            color: #ff1493;
            margin-bottom: 25px;
        }
        .input-group input {
            border-radius: 20px 0 0 20px;
            border: 2px solid #ff69b4;
        }
        .input-group button {
            border-radius: 0 20px 20px 0;
            background-color: #ff69b4;
            border: none;
            color: white;
        }
        .list-group-item {
            border-radius: 15px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #fff0f5;
            border: 1px solid #ffb6c1;
            padding: 10px 15px;
            transition: transform 0.2s;
        }
        .list-group-item:hover {
            transform: scale(1.02);
        }
        .task-completed {
            text-decoration: line-through;
            color: #ff69b4;
        }
        .delete-btn {
            background-color: #ff1493;
            border: none;
            color: white;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            font-size: 0.8rem;
        }
        .delete-btn:hover {
            background-color: #ff69b4;
        }
        .task-icon {
            width: 25px;
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>🌸 My To-Do App 🌸</h2>
        <p>A cute app I built for my convenience 💖 — evolving according to my needs!</p>
        
        <div class="input-group mb-3">
            <input type="text" id="taskInput" class="form-control" placeholder="Add a new task ✨">
            <button id="addBtn">Add</button>
        </div>
        <ul class="list-group" id="taskList"></ul>
    </div>

    <script>
        const taskInput = document.getElementById('taskInput');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');

        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        renderTasks();

        addBtn.addEventListener('click', () => {
            const taskText = taskInput.value.trim();
            if(taskText !== '') {
                tasks.push({ text: taskText, completed: false });
                saveTasks();
                renderTasks();
                taskInput.value = '';
            }
        });

        function renderTasks() {
            taskList.innerHTML = '';
            tasks.forEach((task, index) => {
                const li = document.createElement('li');
                li.className = 'list-group-item';
                
                const span = document.createElement('span');
                span.innerHTML = `🌸 ${task.text}`;
                if(task.completed) span.classList.add('task-completed');

                span.addEventListener('click', () => {
                    tasks[index].completed = !tasks[index].completed;
                    saveTasks();
                    renderTasks();
                });

                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-btn';
                deleteBtn.textContent = '×';
                deleteBtn.addEventListener('click', () => {
                    tasks.splice(index, 1);
                    saveTasks();
                    renderTasks();
                });

                li.appendChild(span);
                li.appendChild(deleteBtn);
                taskList.appendChild(li);
            });
        }

        function saveTasks() {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }
    </script>
</body>
</html>
# To-Do-List
