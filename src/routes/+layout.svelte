<script lang="ts">
	import { page } from '$app/stores';

	// Skeleton Features
	import { AppShell, AppBar, LightSwitch } from '@skeletonlabs/skeleton';
	import { Drawer, drawerStore } from '@skeletonlabs/skeleton';

	// Local Features
	import Navigation from '$lib/components/Navigation.svelte';

	// Stylesheets
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';
	import '@skeletonlabs/skeleton/styles/all.css';
	import '../app.postcss';
	import Header from '$lib/components/Header.svelte';

	function drawerOpen(): void {
		drawerStore.open({});
	}

	// Reactive Properties
	$: classesSidebarLeft = !$page.error ? 'w-0' : 'w-0 lg:w-64';
</script>

<Header pageName={$page.data.pageName}/>
<!-- Drawer -->
<Drawer>
	<h2 class="p-4">DRAMX</h2>
	<hr />
	<Navigation />
</Drawer>

<!-- App Shell -->
<AppShell slotSidebarLeft="bg-surface-500/5 {classesSidebarLeft}">
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<div class="flex items-center">
					<button class="lg:hidden btn btn-sm mr-4" on:click={drawerOpen}>
						<span>
							<svg viewBox="0 0 100 80" class="fill-token w-4 h-4">
								<rect width="100" height="20" />
								<rect y="30" width="100" height="20" />
								<rect y="60" width="100" height="20" />
							</svg>
						</span>
					</button>
					<strong class="text-xl uppercase">DRAMX</strong>
				</div>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<div class="hidden lg:block">
					<a class="btn btn-sm" href="/">Home</a>
					<a class="btn btn-sm" href="/kdrama">Kdrama</a>
					<a class="btn btn-sm" href="/anime">Anime</a>
				</div>
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Left Sidebar Slot -->
	<svelte:fragment slot="sidebarLeft">
		<Navigation />
	</svelte:fragment>
	
	<!-- Page Route Content -->
	<slot />
</AppShell>
