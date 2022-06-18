<script>
	import { enhance } from '$lib/form';
	import { scale } from 'svelte/transition';
	import { flip } from 'svelte/animate';

	export let todos;
</script>

<svelte:head>
	<title>Todos</title>
</svelte:head>

<section class="section">
	<div class="container">
		<div class="box">
			<h1 class="is-size-1 has-text-primary has-text-centered">TODO</h1>

			<form
				class="new"
				action="/todos"
				method="post"
				use:enhance={{
					result: async ({ form }) => {
						form.reset();
					}
				}}
			>
				<input name="text" aria-label="Add todo" placeholder="+ tap to add a todo" />
			</form>

			<!-- -->

			{#each todos as todo (todo.uid)}
		<div
			class="todo has-background-primary"
			class:done={todo.done}
			transition:scale|local={{ start: 0.7 }}
			animate:flip={{ duration: 200 }}
		>
			<form
				action="/todos?_method=PATCH"
				method="post"
				use:enhance={{
					pending: ({ data }) => {
						todo.done = !!data.get('done');
					}
				}}
			>
				<input type="hidden" name="uid" value={todo.uid} />
				<input type="hidden" name="done" value={todo.done ? '' : 'true'} />
				<button class="toggle" aria-label="Mark todo as {todo.done ? 'not done' : 'done'}" />
			</form>

			<form class="text" action="/todos?_method=PATCH" method="post" use:enhance>
				<input type="hidden" name="uid" value={todo.uid} />
				<input aria-label="Edit todo" type="text" name="text" value={todo.text} />
				<button class="save" aria-label="Save todo" />
			</form>

			<form
				action="/todos?_method=DELETE"
				method="post"
				use:enhance={{
					pending: () => (todo.pending_delete = true)
				}}
			>
				<input type="hidden" name="uid" value={todo.uid} />
				<button class="delete" aria-label="Delete todo" disabled={todo.pending_delete} />
			</form>
		</div>
	{/each}

		</div>
	</div>
</section>

<style>
	.todos {
		width: 100%;
		max-width: var(--column-width);
		margin: var(--column-margin-top) auto 0 auto;
		line-height: 1;
	}

	.new {
		margin: 0 0 0.5rem 0;
	}

	input {
		border: 1px solid transparent;
		background: rgba(255, 255, 255, 0.223);
		border-radius: 8px;
	}

	input:focus-visible {
		box-shadow: inset 1px 1px 6px rgba(0, 0, 0, 0.1);
		border: 1px solid #ff3e00 !important;
		outline: none;
	}

	.new input {
		font-size: 28px;
		width: 100%;
		padding: 0.5em 1em 0.3em 1em;
		box-sizing: border-box;
		background: rgba(255, 255, 255, 0.05);
		border-radius: 8px;
		text-align: center;
	}

	.todo {
		display: grid;
		grid-template-columns: 2rem 1fr 2rem;
		grid-gap: 0.5rem;
		align-items: center;
		margin: 0 0 0.5rem 0;
		padding: 0.5rem;
		background-color: pink;
		border-radius: 8px;
		filter: drop-shadow(2px 4px 6px rgba(0, 0, 0, 0.1));
		transform: translate(-1px, -1px);
		transition: filter 0.2s, transform 0.2s;
	}

	.done {
		transform: none;
		opacity: 0.4;
		filter: drop-shadow(0 0 1px rgba(0, 0, 0, 0.1));
	}

	form.text {
		position: relative;
		display: flex;
		align-items: center;
		flex: 1;
	}

	.todo input {
		flex: 1;
		padding: 0.5em 2em 0.5em 0.8em;
		border-radius: 3px;
		opacity: 0.8;
	}

	.todo button {
		width: 2em;
		height: 2em;
		border: none;
		background-color: transparent;
		background-position: 50% 50%;
		background-repeat: no-repeat;
	}

	button.toggle {
		border: 1px solid rgba(0, 0, 0, 0.2);
		border-radius: 50%;
		box-sizing: border-box;
		background-size: 1em auto;
	}

	.done .toggle {
		background-image: url("data:image/svg+xml,%3Csvg width='22' height='16' viewBox='0 0 22 16' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M20.5 1.5L7.4375 14.5L1.5 8.5909' stroke='%23676778' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");
	}

	.delete {
		opacity: 0.3;
		background-color: black !important;
		border: 1rem black;
	}

	.delete:hover,
	.delete:focus {
		transition: opacity 0.2s;
		opacity: 1;
	}

	.save {
		position: absolute;
		right: 0;
		opacity: 0;
		}

	.todo input:focus + .save,
	.save:focus {
		transition: opacity 0.2s;
		opacity: 1;
	}
</style>
