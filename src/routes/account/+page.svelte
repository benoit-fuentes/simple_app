<script lang="ts">
	import { enhance } from '$app/forms';
	import type { SubmitFunction } from '@sveltejs/kit';

	// ...

	let { data, form } = $props()
	let {user, supabase } = $derived(data)
	let profileForm: HTMLFormElement
	let loading = $state(false)

	// ...

	const handleSignOut: SubmitFunction = () => {
		loading = true
		return async ({ update }) => {
			loading = false
			update()
		}
	}
</script>

<h1 class="header">Simple App</h1>
<div>
	You are logged as {user.email}
	<form class="inline" method="post" action="?/signout" use:enhance={handleSignOut}>
		<button disabled={loading}>Sign Out</button>
	</form>
</div>

<style>
	form.inline {
		display: inline-block;
	}
</style>