<script>
	import { createEventDispatcher } from 'svelte';

	export let currentPage = 1;
	export let totalPages;

	const dispatch = createEventDispatcher();

	const handleClick = (page) => {
		currentPage = page;
		dispatch('currentPageChange', currentPage);
	};
</script>

<div class="pagination">
	<button
		class="pagination__button pagination__prev"
		disabled={currentPage === 1}
		on:click={() => handleClick(currentPage - 1)}
	>
		Previous
	</button>

	<button
		class="pagination__button {currentPage === 1
			? 'pagination__button--active'
			: ''} {totalPages === 1 || totalPages === 0 ? 'd-none' : ''}"
		disabled={currentPage === 1}
		on:click={() => handleClick(1)}
	>
		1
	</button>

	{#if currentPage > 3}
		<div style="background-color: #2B2E3133;" class="py-3 h-100">
			<span class="pagination__ellipsis">...</span>
		</div>
	{/if}

	{#each Array.from({ length: totalPages - 2 }, (_, i) => i + 2) as page}
		{#if currentPage === page}
			<button
				class="pagination__button pagination__button--active"
				on:click={() => handleClick(page)}
			>
				{page}
			</button>
		{:else if Math.abs(currentPage - page) < 2}
			<button class="pagination__button" on:click={() => handleClick(page)}>
				{page}
			</button>
		{/if}
	{/each}

	{#if currentPage < totalPages - 2}
		<div style="background-color: #2B2E3133;" class="py-3 h-100">
			<span class="pagination__ellipsis">...</span>
		</div>
	{/if}

	<button
		class="pagination__button {currentPage === totalPages ? 'pagination__button--active' : ''}"
		disabled={currentPage === totalPages}
		on:click={() => handleClick(totalPages)}
	>
		{totalPages}
	</button>

	<button
		class="pagination__next pagination__button"
		disabled={currentPage === totalPages}
		on:click={() => handleClick(currentPage + 1)}
	>
		Next
	</button>
</div>

<style>
	.pagination {
		display: flex;
		justify-content: end;
		margin: 0.2rem 0;
		font-family: myFirstFont;
	}

	.pagination__button {
		background-color: #494949;
		border: 0px;
		color: #000;
		cursor: pointer;
		font-size: 0.85rem;
		/* margin: 0 0.5rem; */
		padding: 0.4rem 0.5rem;
		font-family: myFirstFont;
	}

	.pagination__next {
		background-color: #929292;
		border-radius: 0px 2px 2px 0px;
		color: #000;
	}

	.pagination__prev {
		background-color: #929292;
		border-radius: 2px 0px 0px 2px;
		color: #000;
	}

	.pagination__next:disabled {
		opacity: 50%;
		cursor: default;
	}

	.pagination__prev:disabled {
		opacity: 50%;
		cursor: default;
	}

	.pagination__button:hover:not([disabled]) {
		background-color: #494949;
		color: #000;
	}

	.pagination__button--active {
		background-color: #494949;

		color: #fff;
		padding: 0.3rem 0.7rem;
	}

	.pagination__ellipsis {
		margin: 0 1rem;
		color: #fff;
	}
</style>
