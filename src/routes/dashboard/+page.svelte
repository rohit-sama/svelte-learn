<script>
  import { authHandlers } from "../../store/store";

  let todoLIst = ["learn svelte"];
  let curr = "";
  let error = false;

  function AddTodo() {
    error = false;
    if (curr) {
      todoLIst = [...todoLIst, curr];
      curr = "";
      console.log(todoLIst);
    } else {
      error = true;
    }
  }

  function editTOdo(index) {
    let newTOdo = todoLIst.filter((val, i) => {
      return i !== index;
    });
    curr = todoLIst[index];
    todoLIst = newTOdo;
  }

  function deleteTodo(index) {
    let newTOdo = todoLIst.filter((val, i) => {
      return i !== index;
    });
    todoLIst = newTOdo;
  }
</script>

<div class="mainContainer">
  <div class="headerContainer">
    <h1>Todo</h1>
    <div class="headerButton">
        <button> <i class="fa-regular fa-floppy-disk" />Save</button>

        <button on:click={authHandlers.signout}> <i class="fa-solid fa-right-from-bracket" />Sign Out</button>
    </div>
   
  </div>
  <main>
    {#if todoLIst.length > 0}
    {#each todoLIst as todo, index}
      <div class="todo">
        <p>
          {index + 1}. {todo}
        </p>
        <div class="actions">
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <i on:click={() => {
            editTOdo(index)
          }} on:keydown={() => {}} class="fa-regular fa-pen-to-square"></i>
          <!-- svelte-ignore a11y-no-static-element-interactions -->
          <i  on:click={() => {
            deleteTodo(index)
          }} on:keydown={() => {}} class="fa-regular fa-trash-can"></i>
        </div>
      </div>
    {/each}
{:else}
<p>nothing to show here !!</p>

    {/if}
  </main>
  <div class="enterTodo {error ? 'errorBorder' : ''}">
    <input bind:value={curr} type="text" placeholder="ENter Todo" />
    <button on:click={AddTodo}> Add</button>
  </div>
</div>

<style>
  .mainContainer {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    gap: 24px;
    padding: 24px;
    width: 100%;
    max-width: 1000px;
    margin: 0 auto;
  }

  .headerContainer {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .headerButton {
    display: flex;
    align-items: center;
    gap: 14px;
  }

  .headerContainer button {
    background: #003c5b;
    color: white;
    padding: 10px 18px;
    border: none;
    border-radius: 4px;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 10px;
    cursor: pointer;
  }

  .headerContainer button i {
    font-size: 1.1rem;
  }

  .headerContainer button:hover {
    opacity: 0.7;
  }

  main {
    display: flex;
    flex-direction: column;
    gap: 8px;
    flex: 1;
  }

  .enterTodo {
    display: flex;
    align-items: stretch;
    border: 1px solid #0891b2;
    border-radius: 5px;
    overflow: hidden;
  }

  .errorBorder {
    border-color: coral !important;
  }

  .enterTodo input {
    background: transparent;
    border: none;
    padding: 14px;
    color: white;
    flex: 1;
  }

  .enterTodo input:focus {
    outline: none;
  }

  .enterTodo button {
    padding: 0 28px;
    background: #003c5b;
    border: none;
    color: cyan;
    font-weight: 600;
    cursor: pointer;
  }

  .enterTodo button:hover {
    background: transparent;
  }

  .todo {
    border-left: 1px solid cyan;
    padding: 8px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .actions {
    display: flex;
    align-items: center;
    gap: 14px;
    font-size: 1.3rem;
  }

  .actions i {
    cursor: pointer;
  }

  .actions i:hover {
    color: coral;
  }
</style>
