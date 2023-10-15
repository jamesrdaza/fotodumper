<script>
    export let username = "Profile";
</script>

<nav>
    <div class="leftNav">
            <a style="margin-left: 15px;" href="/">fotodumper</a>
            <a href="/upload">Upload</a>
    </div>
    <div class="rightNav">
        <div style="margin-right: 15px; "class="dropdown">
            <a href={username === "Profile" ? "http://localhost:5173/profile" : `http://localhost:5173/profile/${username}`}>{username}</a>
            <div class="dropdownLinks">
                <a class="link" href="http://localhost:3000/logout">Logout</a>
            </div>
        </div>
    </div>
</nav>

<style>
    nav {
        height: 60px;
        display: flex;
        grid-column: span 12; 
    }
    
    li {
        list-style-type: none;
    }
    
    .leftNav, .rightNav{
        height: 100%;
        width: 100%;
        display: flex;
        gap: 15px;
        align-items: center;
    }
    
    .leftNav {
        justify-content: left;
    }

    .rightNav {
        justify-content: right;
    }
    
    .dropdown {
        position: relative;
        z-index: 2;
    }
    .dropdownLinks {
        display: none;
        position: absolute;
    }
    .dropdown:hover .dropdownLinks {
        display: block;
    }
    .link {
        margin-top: 5px;
        display: block;
        border-radius: 5px;
        height: 40px;
        line-height: 40px;
        padding: 2px;
    } 
    
    .link {
        border: 1px solid grey;
    }

    
</style>