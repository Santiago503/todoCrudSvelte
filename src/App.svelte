<script>
  let todos = [];
  let todo = { id: "", text: "", estado: false };

  const nameStorage = "todos";

  if (localStorage.getItem("todos")) {
    todos = JSON.parse(localStorage.getItem("todos"));
  }

  const addTodo = () => {
    if (!todo.text) {
      return;
    }

    todo.id = Date.now();
    todos = [...todos, todo];
    todo = { id: "", text: "", estado: false };
  };

  $: localStorage.setItem(nameStorage, JSON.stringify(todos));

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
        ...item,
      };
    });

  };

  $: classIcon = (valor) => (valor ? "bi bi-arrow-clockwise" : "bi bi-check2");

  const classEstado = (valor) => (valor ? "btn-success" : "btn-warning");
</script>

<div class="container">
  <h1 class="display-5 my-3 text-center">
    <h1>Hola Mundo Todo en Svelte</h1>
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
      <p
        class={(td.estado
          ? "text-decoration-line-through"
          : "") + " text-capitalize"}
      >
        {td.text}
      </p>
      <div>
        <button
          class="btn btn-sm {classEstado(td.estado)}"
          on:click={editTodo(td.id)}
        >
          <i class={classIcon(td.estado)} />
        </button>
        <button class="btn btn-sm btn-danger" on:click={delTodo(td.id)}
          ><i class="bi bi-trash" /></button
        >
      </div>
    </div>
  {/each}
</div>
