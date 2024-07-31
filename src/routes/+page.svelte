<script lang="ts">
	type Todo = {
		id: number;
		content: string;
		completed: boolean;
	};

	let newTodo = '';

	let todos: Todo[] = [];

	let initId = 1;

	const addTodo = () => {
		todos = [...todos, { id: initId++, content: newTodo, completed: false }];
		newTodo = '';
	};

	const removeTodo = (targetId: number) => {
		todos = todos.filter((todo) => todo.id !== targetId);
	};
</script>

<h1>Todo List <span class="sub-title">powered by Svelte</span></h1>
<form on:submit|preventDefault={addTodo}>
	<input bind:value={newTodo} type="text" placeholder="Add a todo" />
	<button type="submit">Add</button>
</form>
<ul>
	{#each todos as todo (todo.id)}
		<li>
			<input
				type="checkbox"
				id={todo.id.toString()}
				class="todo"
				on:click={() => {
					todo.completed = todo.completed ? false : true;
				}}
			/>
			<label for={todo.id.toString()} class={`${todo.completed ? 'checked' : ''}`}>
				{todo.content}
			</label>
			<button type="button" class="btn-delete" on:click={() => removeTodo(todo.id)}>✖︎</button>
		</li>
	{/each}
</ul>

<style>
	li {
		list-style: none;
	}

	span.sub-title {
		display: block;
		font-size: 0.7rem;
	}

	label.checked {
		transition: ease-in-out 0.1s;
		text-decoration: line-through;
		color: #d0d0d0;
	}

	button.btn-delete {
		background-color: #ededed;
		border: none;
		border-radius: 5px;
	}

	button.btn-delete:hover {
		transition: ease-in-out 0.1s;
		cursor: pointer;
		background-color: #d0d0d0;
	}
</style>
