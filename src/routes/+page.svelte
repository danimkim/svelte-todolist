<script lang="ts">
	let todos: string[] = ['Do the laundry', 'Wash the dishes', 'Take out the trash'];
</script>

<h1>Todo List <span class="sub-title">powered by Svelte</span></h1>
<form>
	<input type="text" placeholder="Add a todo" />
	<button type="button">Add</button>
</form>
<ul>
	<!-- Todo will be rendered here -->
	{#each todos as todo}
		<li>{todo}</li>
	{/each}
</ul>

<style>
	span.sub-title {
		display: block;
		font-size: 0.7rem;
	}
</style>
