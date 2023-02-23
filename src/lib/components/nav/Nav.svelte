<script>
	import { Disclosure, DisclosureButton, DisclosurePanel } from '@rgossiaux/svelte-headlessui';
	import Cancel from '../icon/Cancel.svelte';
	import Logo from '../icon/Logo.svelte';
	import Menu from '../icon/Menu.svelte';
	import { page } from '$app/stores';

	let links = [
		{ name: 'Products', href: '/products' },
		{ name: 'Categories', href: '/categories' },
		{ name: 'Inspiration', href: '/inspiration' },
		{ name: 'Thoughts', href: '/thoughts' }
	];
</script>

<Disclosure as="nav" let:open class="px-4 py-4 md:px-8 lg:py-10">
	<div class="mx-auto max-w-5xl">
		<div class="relative flex h-16 items-center justify-between">
			<div class="flex flex-1 items-center justify-between">
				<a
					class="focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-orange-400"
					href="/"><Logo class="h-6 w-auto text-slate-900" /></a
				>
				<div class="hidden space-x-12 lg:flex">
					{#each links as { name, href }}
						<a
							class="{$page.url.pathname === href
								? 'text-orange-500'
								: 'text-slate-900'} text-base font-normal hover:text-orange-500 focus-visible:text-orange-500 focus-visible:underline focus-visible:outline-none"
							{href}>{name}</a
						>
					{/each}
				</div>
				<DisclosureButton
					class="rounded-md p-1 text-slate-900 hover:bg-slate-200 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-orange-400 lg:hidden"
				>
					<span class="sr-only">Open main menu</span>
					{#if open}
						<Cancel class="block h-8 w-8 text-slate-900 md:h-10 md:w-10" />
					{:else}
						<Menu
							class="block h-8 w-8 text-slate-900 group-hover:text-orange-500 md:h-10 md:w-10"
						/>
					{/if}
				</DisclosureButton>
				<a
					class="hidden text-base font-normal text-slate-900 hover:text-orange-500 focus-visible:text-orange-500 focus-visible:underline focus-visible:outline-none lg:inline"
					href="/">Login</a
				>
			</div>
		</div>
	</div>
	<DisclosurePanel class="block border-t-2 border-slate-200 py-6 md:py-8 lg:hidden">
		<ul class="space-y-4 md:space-y-6">
			{#each links as { name, href }}
				<li>
					<DisclosureButton
						as="a"
						{href}
						class="{$page.url.pathname === href
							? 'text-orange-500'
							: 'text-slate-900'} text-base font-normal hover:text-orange-500 focus-visible:text-orange-500 focus-visible:underline focus-visible:outline-none"
					>
						{name}
					</DisclosureButton>
				</li>
			{/each}
			<li>
				<DisclosureButton
					as="a"
					href="/"
					class="text-base font-normal text-slate-900 hover:text-orange-500 focus-visible:text-orange-500 focus-visible:underline focus-visible:outline-none"
				>
					Login
				</DisclosureButton>
			</li>
		</ul>
	</DisclosurePanel>
</Disclosure>
