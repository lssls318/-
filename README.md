<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>简易待办事项应用</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            padding: 30px;
        }
        
        h1 {
            text-align: center;
            margin-bottom: 30px;
            color: #2c3e50;
        }
        
        .input-section {
            display: flex;
            margin-bottom: 30px;
        }
        
        #taskInput {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 5px 0 0 5px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s;
        }
        
        #taskInput:focus {
            border-color: #3498db;
        }
        
        #addBtn {
            padding: 12px 25px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 0 5px 5px 0;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        
        #addBtn:hover {
            background-color: #2980b9;
        }
        
        .filter-section {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }
        
        .filter-btn {
            padding: 8px 15px;
            margin: 0 5px;
            background-color: #ecf0f1;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .filter-btn.active {
            background-color: #3498db;
            color: white;
        }
        
        .task-list {
            list-style-type: none;
        }
        
        .task-item {
            display: flex;
            align-items: center;
            padding: 15px;
            background-color: #f9f9f9;
            border-radius: 5px;
            margin-bottom: 10px;
            transition: all 0.3s;
        }
        
        .task-item:hover {
            background-color: #f0f0f0;
        }
        
        .task-item.completed {
            opacity: 0.7;
            text-decoration: line-through;
        }
        
        .task-text {
            flex: 1;
            margin-left: 10px;
        }
        
        .task-checkbox {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .delete-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .delete-btn:hover {
            background-color: #c0392b;
        }
        
        .empty-state {
            text-align: center;
            padding: 30px;
            color: #7f8c8d;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            .input-section {
                flex-direction: column;
            }
            
            #taskInput {
                border-radius: 5px;
                margin-bottom: 10px;
            }
            
            #addBtn {
                border-radius: 5px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>我的待办事项</h1>
        
        <div class="input-section">
            <input type="text" id="taskInput" placeholder="添加新任务...">
            <button id="addBtn">添加</button>
        </div>
        
        <div class="filter-section">
            <button class="filter-btn active" data-filter="all">全部</button>
            <button class="filter-btn" data-filter="active">待完成</button>
            <button class="filter-btn" data-filter="completed">已完成</button>
        </div>
        
        <ul class="task-list" id="taskList">
            <!-- 任务将在这里动态添加 -->
        </ul>
    </div>

    <script>
        // 从本地存储获取任务或初始化空数组
        let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
        let currentFilter = 'all';

        // DOM元素
        const taskInput = document.getElementById('taskInput');
        const addBtn = document.getElementById('addBtn');
        const taskList = document.getElementById('taskList');
        const filterBtns = document.querySelectorAll('.filter-btn');

        # -
· 添加新任务 · 标记任务为已完成 · 删除任务 · 数据保存在本地存储中 · 响应式设计
