<script lang="ts">
	type Todo = {
		id: number;
		content: string;
		completed: boolean;
	};

	let newTodo = '';

	let todos: Todo[] = [
		{ id: 1, content: 'todo1', completed: false },
		{ id: 2, content: 'todo2', completed: false },
		{ id: 3, content: 'todo3', completed: false }
	];

	const addTodo = () => {
		todos = [...todos, { id: todos.length + 1, content: newTodo, completed: false }];
		newTodo = '';
	};
</script>

<h1>Todo List <span class="sub-title">powered by Svelte</span></h1>
<form on:submit|preventDefault={addTodo}>
	<input type="text" name="todo" placeholder="Add a todo" bind:value={newTodo} />
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
</style>
