<script lang="ts">
    import TodoContainer from './components/TodoContainer.svelte'
    import Header from './components/Header.svelte'

    type Todo = {
        label: string
        completed: boolean
    }

    let inputValue: string = ''
    let todos: Todo[] = []

    function setCompleted(index: number) {
        todos[index].completed = !todos[index].completed
        todos = todos
    }

    function clearCompleted() {
        todos = todos.filter(todo => !todo.completed)
    }

    function addTodo() {
        todos.push({
            label: inputValue,
            completed: false
        })
        todos = todos
        inputValue = ''
    }
</script>

<TodoContainer>
    <Header />
    <ol>
        {#each todos as { label, completed }, index}
            <li class:completed={completed} on:click={() => setCompleted(index)}>
                {label}
            </li>
        {/each}
    </ol>
    <button on:click={clearCompleted}>Clear Completed</button>
    <div>
        <input type="text" bind:value={inputValue} placeholder="Enter Task">
        <button on:click={addTodo}>OK</button>
    </div>
</TodoContainer>

<style>
    ol {
        display: flex;
        flex-direction: column;
        gap: 10px;
        padding-inline-start: 17px;
    }

    li {
        cursor: pointer;
    }

    li.completed {
        text-decoration: line-through;
    }

    input:focus-visible {
        outline-color: #ff3e00;
    }
</style>