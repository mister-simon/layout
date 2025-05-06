<script>
	const links = ['Home', 'About Me', 'About You', 'About Your Mum'];
	let popover = $state();
	const kebabCase = (string) =>
		string
			.replace(/([a-z])([A-Z])/g, '$1-$2')
			.replace(/[\s_]+/g, '-')
			.toLowerCase();
</script>

{#snippet navLink(href, name)}
	<li class="scrollspy" style:animation-timeline={`--${kebabCase(name)}`}>
		<a href={`#${href}`} onclick={() => popover.hidePopover()}>{name}</a>
	</li>
{/snippet}

{#snippet navigation()}
	<ul>
		{#each links as item}
			{@render navLink(item, item)}
		{/each}
	</ul>
{/snippet}

<div class="layout">
	<header class="navbar col-span-12 h-(--nav-height)">
		<div class="flex w-full">
			<h1>Nice Layout</h1>
			<button popovertarget="mobile-nav" class="mobile-nav-btn ml-auto block lg:hidden"
				>Open / Close Nav</button
			>
		</div>
	</header>
	<nav popover id="mobile-nav" class="mobile-nav lg:hidden" bind:this={popover}>
		{@render navigation()}
	</nav>
	<aside class="desktop-nav col-span-3 max-lg:hidden">
		<div class="desktop-nav-inner">
			{@render navigation()}
		</div>
	</aside>
	<main class="content col-span-12 lg:col-span-9">
		{#each links as item}
			<section
				id={item}
				style:scroll-timeline-name={`--${kebabCase(item)}`}
				style:scroll-timeline-axis="block"
			>
				<div class="prose mx-auto">
					<h2>{item}</h2>
					<p>
						Lorem ipsum dolor, sit amet consectetur adipisicing elit. Doloremque ipsam cupiditate,
						voluptatum voluptates ad suscipit sequi delectus. Repudiandae, eveniet ratione ab quis
						tenetur consectetur natus rem laborum, expedita consequuntur corporis.
					</p>
					<p>
						Lorem ipsum dolor, sit amet consectetur adipisicing elit. Doloremque ipsam cupiditate,
						voluptatum voluptates ad suscipit sequi delectus. Repudiandae, eveniet ratione ab quis
						tenetur consectetur natus rem laborum, expedita consequuntur corporis.
					</p>
					<p>
						Lorem ipsum dolor, sit amet consectetur adipisicing elit. Doloremque ipsam cupiditate,
						voluptatum voluptates ad suscipit sequi delectus. Repudiandae, eveniet ratione ab quis
						tenetur consectetur natus rem laborum, expedita consequuntur corporis.
					</p>
				</div>
			</section>
		{/each}
	</main>
</div>

<style>
	:global(html) {
		--nav-height: 4rem;
		scroll-padding-block-start: calc(var(--nav-height, 0px) + 5svh);
	}

	.layout {
		position: relative;
		display: grid;
		grid-template-rows: auto auto;
		grid-template-columns: repeat(12, minmax(0, 1fr));
		column-gap: 1rem;
		isolation: isolate;
	}
	.navbar {
		z-index: 1;
		position: sticky;
		top: 0;
		anchor-name: --navbar;
		grid-row: 1 / 2;
	}

	.mobile-nav {
		position: absolute;
		top: anchor(--navbar bottom);
		bottom: 0px;
		width: max(min(100%, 500px), 75vw);
		margin-left: auto;
		height: auto;

		&::backdrop {
			top: anchor(--navbar bottom);
			background: rgb(0 0 0 / 0.7);
		}
	}

	.desktop-nav-inner {
		position: sticky;
		max-height: calc(100dvh - var(--nav-height));
		top: var(--nav-height);
		overflow-block: auto;
	}

	/* Styles */
	.layout {
		--bg: black;
		background-color: var(--bg);
	}
	.navbar {
		background: var(--color-orange-950);
		color: white;
		display: flex;
		align-items: center;
		padding: 1rem;
		border-bottom: 1rem solid var(--bg);
	}

	.mobile-nav {
		border-left: 1rem solid var(--bg);
		padding: 1rem;
	}

	.mobile-nav,
	.desktop-nav {
		background-color: var(--color-teal-900);
		color: white;
	}

	.desktop-nav-inner {
		padding: 1rem;
		scrollbar-color: var(--color-teal-900) var(--bg);
	}

	.content {
		display: grid;
		row-gap: 1rem;
		/* background-color: color-mix(in oklch, var(--bg), var(--color-amber-100)); */
		background-color: var(--bg);

		section {
			background-color: var(--color-amber-100);
			border: 1px solid black;
			padding-block: calc(5rem / 2);
		}
	}

	.scrollspy {
		border-left: 1rem solid transparent;
		animation-name: scrollspy;
	}

	@keyframes scrollspy {
		0% {
			border-left-color: transparent;
		}
		50% {
			border-left-color: black;
		}
		100% {
			border-left-color: transparent;
		}
	}
</style>
