<script>
  let todos = [];
  let todo = { id: "", text: "", estado: false };

  const addTodo = () => {
    if (!todo.text) {
      return;
    }

    todo.id = Date.now();
    todos = [...todos, todo];
    console.log(todo);
    todo = { id: "", text: "", estado: false };
  };
  const delTodo = (id) => {
    todos = todos.filter((item) => item.id !== id);
  };
  const editTodo = (id) => {
    todos = todos.map((item) => {
      if (item.id === id) {
        return {
          ...item,
          estado: !item.estado,
        };
      }

      return {
        item,
      };
    });
  };
</script>

<div class="container">
  <h1 class="display-5 my-3">
    <h1>Hola Mundo</h1>
  </h1>

  <form on:submit|preventDefault={addTodo}>
    <input
      type="text"
      placeholder="Enter para agregar todo"
      class="form-control shadow-sm border-0"
      bind:value={todo.text}
    />
  </form>

  {#each todos as td}
    <div class="shadow my-3 p-3 lead d-flex justify-content-between">
      <p>{td.text}</p>
      <div>
        <button class="btn btn-sm btn-warning" on:click={editTodo(td.id)}
          ><i class="bi bi-pen" /></button
        >
        <button class="btn btn-sm btn-danger" on:click={delTodo(td.id)}
          ><i class="bi bi-trash" /></button
        >
      </div>
    </div>
  {/each}
</div>
