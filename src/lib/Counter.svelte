<script>
	import { spring } from "svelte/motion";

	let count = 0;

	const displayed_count = spring();
	$: displayed_count.set(count);
	$: offset = modulo($displayed_count, 1);

	function modulo(n, m) {
		// handle negative numbers
		return ((n % m) + m) % m;
	}
</script>

<section class="section">
	<div class="container is-max-desktop">
		
		<div class="box">
			<div class="has-text-centered has-text-weight-bold has-text-primary mb-4"><h1 class="text-center is-size-1">Counter</h1></div>
	
			<div class="is-flex is-justify-content-center">
				<button
					class="button is-primary is-small"
					on:click={() => (count -= 1)}
				>
					-
				</button>
				<div
					class="mx-4"
					style="transform: translate(0, {100 * offset}%)"
				>
					<strong
						class="hidden is-size-4"
						style="color: white;"
						aria-hidden="true"
						>{Math.floor($displayed_count + 1)}</strong
					>
				</div>
				<button
					class="button is-primary is-small"
					on:click={() => (count += 1)}
				>
					+
				</button>
			</div>
		</div>
	</div>
</section>
