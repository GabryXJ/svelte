<script>
  let newTask = '';
  let tasks = [];

  function addTask() {
    if (newTask.trim() !== '') {
      tasks = [...tasks, { text: newTask, completed: false }];
      newTask = '';
    }
  }

  function deleteTask(){
    tasks = tasks.filter(task => task !== tasks[tasks.indexOf(task)]);
  }


  function toggleComplete(index) {
    tasks = tasks.map((task, i) => 
      i === index ? { ...task, completed: task.completed } : task
    );
  }

  function removeTask(index) {
    tasks = tasks.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1>To-Do List</h1>
  <input bind:value={newTask} placeholder="Add a new task" />
  <button on:click={addTask}>Add Task</button> 
  <button on:click={deleteTask}>Remove al Task</button>

  <ul>
    {#each tasks as task, index}
      <li>
        <input type="checkbox" bind:checked={task.completed} on:change={() => toggleComplete(index)} />
        <span style="text-decoration: {task.completed ? 'line-through' : 'none'}">{task.text}</span>
        <button on:click={() => removeTask(index)}>Remove</button>
      </li>
    {/each}
  </ul>
</main>

<style>
  main {
    font-family: Arial, sans-serif;
    margin: 0 auto;
    max-width: 400px;
    text-align: center;
    padding: 20px;
  }

  input {
    margin: 0.5em;
    padding: 0.5em;
    font-size: 1em;
  }

  button {
    margin: 0.5em;
    padding: 0.5em 1em;
    font-size: 1em;
  }

  ul {
    list-style: none;
    padding: 0;
    background-color: rgb(136, 136, 136);
    border-radius: 10px;
  }

  li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 0.5em 0;
  }

  span {
    flex: 1;
    margin: 0 1em;
  }
</style>
