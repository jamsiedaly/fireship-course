<script lang="ts">
    import AuthCheck from "$lib/components/AuthCheck.svelte";
    import {supabase} from "../../../lib/supabaseClient";
    export let data;

    let username = "";
    let loading = false;
    let isAvailable = false;

    let debounceTimer: NodeJS.Timeout;

    async function checkAvailability() {
        isAvailable = false;
        loading = true;
        clearTimeout(debounceTimer);

        debounceTimer = setTimeout(async () => {
            supabase.from('users').select('name').eq('name', username).then(({data, error}) => {
                if (error) {
                    return;
                } else {
                    console.log(data);
                    isAvailable = true;
                }
            });
            loading = false;
        }, 500);

    }

    async function confirmUsername() {
        if (!loading && isAvailable) {
            supabase.from('users').insert({'email': data.session.user.email, 'name': username}).then(({data, error}) => {
                if (error) {
                    return;
                } else {
                    console.log(data);
                }
            });
        }
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
