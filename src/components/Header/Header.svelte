<script>
    import { username, user } from '../../utils/users';

    function signout() {
        user.leave()
        username.set('')
    }
</script>

<header class="header-style">
    <h1>De-Chat</h1>
    {#if $username}
        <div class="user-bio">
            <span>Hello <strong>{$username}</strong></span>
            <img src={`https://avatars.dicebear.com/api/initials/${$username}.svg`} alt="avatar"  />
        </div>
        <button class="signout-button" on:click={signout}>Sign Out</button>
    {:else}
        <h3>Decentralized Chat</h3>
    {/if}
</header>

<style>
    .header-style {
        background-color: rgb(111, 40, 197);
        height: 10vh;
        min-height: 50px;
        color: white;
        position: fixed;
        width: 100%;
        max-width: 728px;
        top: 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
        z-index: 99;
        padding: 10px;
        box-sizing: border-box;
    }

    .signout-button {
        font-size: 0.8rem;
        padding: 0.5rem 1rem;
        background-color: rgba(247, 247, 247, 0.788);
        color:rgb(111, 40, 197);
        font-weight: bold;
    }
</style>