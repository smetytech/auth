<script lang="ts">
	import { page } from '$app/stores';
	import { ArrowLeft } from 'lucide-svelte';
	import { Button } from '$lib/components/ui/button';

	let { children } = $props();

	let isSignUpRoute = $derived($page.route.id === '/auth/sign-up');
	let isSignInRoute = $derived($page.route.id === '/auth/sign-in');

	function handleBackButtonClick() {
		history.back();
	}
</script>

<div
	class="mx-auto flex min-h-screen max-w-[80rem] grow flex-col justify-between gap-12 p-6 lg:p-10"
>
	<div class="flex items-center justify-between">
		<Button variant="ghost" onclick={handleBackButtonClick}>
			<ArrowLeft class="!h-5 !w-5" />
			<span>Back</span>
		</Button>

		{#if isSignUpRoute}
			<Button variant="ghost" href="/auth/sign-in">
				<span>Sign In</span>
			</Button>
		{:else if isSignInRoute}
			<Button variant="ghost" href="/auth/sign-up">
				<span>Sign Up</span>
			</Button>
		{/if}
	</div>

	<div class="mx-auto w-full max-w-sm grow lg:flex lg:items-center">
		{@render children()}
	</div>
</div>
