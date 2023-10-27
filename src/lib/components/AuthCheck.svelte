<script lang="ts">
    export let data
</script>

{#if data.session}
    <slot />
{:else}
    <p class="text-error">You must sign in before choosing a user name.</p>
        <a class="btn btn-primary" href="/login">Sign in</a>
{/if}