<div class="home">
    <div class="imageContainer">
        <img src="./photo.svg" alt="">
    </div>
    <div class="side">
        <h2>Dump Fotos.</h2>
        <a href="/upload">
            <div class="continue">
                ->
            </div>
        </a>
    </div>
</div>

<style>
    .home {
        height: calc(100vh - 60px);
        grid-column: span 12;
        
        display: flex;
    }
    .imageContainer {
        width: 60%;
        
        display: flex;
        justify-content: center;
        align-items: center;
    }
    img {
        max-width: 70%;
        height: auto;
    }
    .side {
        position: relative;
        width: 40%;
        text-align: center;
        
        display:flex;
        justify-content: center;
        align-items: center;
    }
    h2 {
        font-size: 40px;
        height: 40%;
    }
    .continue {
        position: absolute;
        width: 70px;
        height: 70px;
        line-height: 70px;
        border: 1px solid grey;
        border-radius: 5px;
        
        bottom: 70px;
        right: 50px;
        transition: 0.25s;
    }
    .continue:hover {
        border: 1px solid rgba(173, 216, 230, 0.308);
        transition: 0.25s;
    }
</style>