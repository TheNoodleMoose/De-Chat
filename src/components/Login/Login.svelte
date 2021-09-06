<script>
    import { user } from '../../utils/users';

    let username;
    let password;

    function login() {
        user.auth(username, password, ({err}) => err && alert(err))
    }

    function signup() {
        user.create(username, password, ({err}) => {
            if (err) {
                alert(err);
            } else {
                login()
            }
        })
    }
 </script>
    <div class="content-container">
        <label for="username" class="label-style">Username</label>
        <input name="username" bind:value={username} minlength="3" maxLength="16" class="input-style" />
    
        <label for="password" class="label-style">Password</label>
        <input name="password" bind:value={password} type="password" class="input-style" />
    </div>
    <div class="content-container">
        <button class="login" on:click={login}>Login</button>
        <button class="login" on:click={signup}>Sign Up</button>
    </div>

 <style>
     .label-style {
        color: rgb(111, 40, 197);
        font-size: 1.3rem;
        font-weight: bold;
        margin: 0.5rem 0;
     }

     .content-container {
         display: flex;
         justify-content: center;
         align-items: center;
         flex-direction: column;
     }

     .login {
        padding: 0.25em 0.75em;
         width: 90%;
        min-height: 44px;
        border-radius: 20px;
        margin: 1rem 0 0;
        background: #6f28c5;
        box-shadow: 0px 0px 17px 0px rgba(50, 50, 50, 0.75);
     }

     .input-style {
        line-height: 1.5;
        width: 90%;
        font-size: 1.5rem;
        background: rgb(209, 209, 209);
        color: rgb(0, 0, 0);
        /* outline: none; */
        /* border: none; */
        padding: 0 10px;
        margin: 0;
        border-radius: 10px;
     }
 </style>
