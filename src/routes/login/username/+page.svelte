<script>
    import AuthCheck from "$lib/components/AuthCheck.svelte";
    export let data;

    let username = "";
    let loading = false;
    let isAvailable = false;

    async function checkAvailability() {

    }

    async function confirmUsername() {
        // TODO
    }
</script>

<AuthCheck data={data}>
    <h2>Username</h2>
    <form class="w-2/5" on:submit|preventDefault={confirmUsername}>
        <input
                type="text"
                placeholder="Username"
                class="input w-full"
                bind:value={username}
                on:input={checkAvailability}
        />

        <p>Is available? {isAvailable}</p>

        <button class="btn btn-success">Confirm username @{username} </button>

    </form>
</AuthCheck>
