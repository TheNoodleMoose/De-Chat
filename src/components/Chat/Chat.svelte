<script>
    import GUN, { SEA } from 'gun';
    import { onMount } from 'svelte';
    import { user, username } from '../../utils/users';
    import ChatMessage from '../ChatMessage/ChatMessage.svelte';
    import Login from '../Login/Login.svelte';

    const db = GUN();

    let newMessage;
    let messages = [];
    onMount(() => {
        db.get('de-chat').map().once(async (data, id) => {
            if (data) {
                // Key for end-to-end encryption
                const key = '#foo';
                var message = {
                    // transform the data
                    who: await db.user(data).get('alias'), // a user might lie who they are! So let the user system detect whose data it is.
                    what: (await SEA.decrypt(data.what, key)) + '', // force decrypt as text.
                    when: GUN.state.is(data, 'what'), // get the internal timestamp for the what property.
                };
               
                if (message.what) {
                    messages = [...messages.slice(-100), message].sort((a, b) => a.when - b.when);
                }
            }
        })
    })

    async function sendMessage() {
        const secret = await SEA.encrypt(newMessage, '#foo');
        const message = user.get('all').set({ what: secret });
        const index = new Date().toISOString();
        db.get('de-chat').get(index).put(message);
        newMessage = '';
    }
</script>

<div class="container">
    {#if $username}
        <main>
            {#each messages as message (message.when)}
                <ChatMessage {message} sender={$username} />
            {/each}
        </main>
        <form on:submit|preventDefault={sendMessage}>
            <input type="text" placeholder="Type message here..." bind:value={newMessage} maxlength="100" class="message-style" /> 
            <button type="submit" disabled={!newMessage}>🔥</button>
        </form>
    {:else}
        <main>
            <Login />
        </main>
    {/if}
</div>

<style>
    .message-style {
        width: 80%;
    }

    form {
        height: 8vh;
        position: fixed;
        bottom: 0;
        background-color: rgb(57, 28, 94);
        width: 100%;
        max-width: 728px;
        display: flex;
        font-size: 1.5rem;
    }

    form button {
        width: 20%;
        background-color: rgb(111, 40, 197);
    }
</style>