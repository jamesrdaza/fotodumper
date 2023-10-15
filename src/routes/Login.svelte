<div class="login">
    <a class="" href="http://localhost:3000/login/federated/google">Sign in with Google</a>
</div>

<style>
    .login {
        height: calc(100vh - 60px);
        grid-column: span 12;
        
        display: flex;
        justify-content: center;
        align-items: center;
    }


    a {
        color: white;
        height: 20px;
        padding: 10px;
        border: 1px solid black;
        background-color: #4f87ea;
        border-radius: 5px;
        transition: 0.25s;
        line-height: 20px;
    }
    
    a:hover {
        transition: 0.25s;
        background-color: white;
        color: blue;
    }
</style>