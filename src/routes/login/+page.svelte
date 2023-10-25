<script lang="ts">
    export let data
    let { supabase } = data
    $: ({ supabase } = data)

    const handleSignUp = async () => {
        await supabase.auth.signInWithOAuth({
            provider: 'google',
        })
    }

    const handleSignOut = async () => {
        await supabase.auth.signOut()
    }
</script>

{#if !data.session}
    <h1>Sign In</h1>
    <form on:submit="{handleSignUp}">
        <button class="btn btn-primary">Sign in with Google</button>
    </form>
{:else}
    <h2 class="card-title">Welcome, {data.session.user.email}</h2>
    <p class="text-center text-success">You are logged in</p>
    <a href="/login/username"><button class="btn btn-primary">continue</button> </a>
    <button class="btn btn-warning" on:click={handleSignOut}>Sign out</button>
{/if}