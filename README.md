import React, { useState } from "react";

function TodoApp() {
  const [tasks, setTasks] = useState([]); // list of tasks
  const [input, setInput] = useState(""); // input field state

  // handle input change (onChange)
  const handleChange = (e) => {
    setInput(e.target.value);
  };

  // handle add task (onClick)
  const addTask = () => {
    if (input.trim() !== "") {
      setTasks([...tasks, { text: input, completed: false }]);
      setInput(""); // clear input field
    }
  };

  // handle toggle complete
  const toggleComplete = (index) => {
    const newTasks = [...tasks];
    newTasks[index].completed = !newTasks[index].completed;
    setTasks(newTasks);
  };

  // handle delete task
  const deleteTask = (index) => {
    const newTasks = tasks.filter((_, i) => i !== index);
    setTasks(newTasks);
  };

  return (
    <div style={{ padding: "20px", fontFamily: "Arial" }}>
      <h2>📝 To-Do List</h2>

      <input
        type="text"
        value={input}
        onChange={handleChange}
        placeholder="Enter a task"
      />
      <button onClick={addTask} style={{ marginLeft: "10px" }}>
        Add
      </button>

      <ul>
        {tasks.map((task, index) => (
          <li
            key={index}
            style={{
              textDecoration: task.completed ? "line-through" : "none",
              margin: "5px 0",
            }}
          >
            <span onClick={() => toggleComplete(index)}>{task.text}</span>
            <button
              onClick={() => deleteTask(index)}
              style={{ marginLeft: "10px", color: "red" }}
            >
              ❌
            </button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoApp;
