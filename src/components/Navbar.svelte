<script>

</script>

<nav>
    <div class="leftNav">
            <a style="margin-left: 15px;" href="/"><li>fotodumper</li></a>
            <a href="/"><li>Home</li></a>
    </div>
    <div class="rightNav">
        <a style="margin-right: 15px;" href="/"><li>Profile</li></a>
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
</style>