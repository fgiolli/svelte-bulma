<header>
	<nav class="navbar" aria-label="main navigation">
		<div class="navbar-brand">
		  <a class="navbar-item" href="https://bulma.io">
			<strong>Bulma w Svelte!</strong>
		  </a>

		  
		</div>
	  
		<div class="navbar-menu">
		  <ul class="navbar-start">
			<li class="navbar-item"><a sveltekit:prefetch href="/">Home</a></li>
			
	  
			<li class="navbar-item">
				<a sveltekit:prefetch href="/about">About</a>
			</li>
	  
			<div class="navbar-item has-dropdown is-hoverable">
			  <li class="navbar-link">
				More
			  </li>
	  
			  <ul class="navbar-dropdown">
				<li class="navbar-item">
					<a sveltekit:prefetch href="/todos">Todos</a>
				</li>
			</ul>
			</div>
		</ul>
	  
		</div>
	  </nav>
</header>