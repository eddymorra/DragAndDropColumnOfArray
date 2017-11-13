<template>
    <div>
        <div class="topbar">
            <h1>Gestion de tableau</h1>
        </div>

        <div class="menugauche">
            <ul>
                <li>Menu</li>
                <li>Accueil</li>
                <li>Item menu 2</li>
                <li>Item menu 3</li>
                <li>Item menu 4</li>
                <li>Item menu 5</li>
                <li>Item menu 6</li>
                <li>Item menu 7</li>
                <li>Item menu 8</li>
                <li>Item menu 9</li>
                <li>Dernier Item du menu</li>
            </ul>
        </div>
        <div id="app"> 
            <tab></tab>
        </div>
    </div>
</template>

<script>
    import Tab from './components/Tab';

    export default {
    name: 'app',
    components: {
        'tab': Tab
    }
    }
</script>

<style>

* {
    margin: 0; padding: 0;
    box-sizing: border-box;
    font-family: Source Sans Pro, sans-serif, arial;
}

html {
    background-color: #ffffff;
    width: 100%; height: 100%;
}

.topbar {
    position: fixed;
    width: 100%; height: 42px;
    background-color: #222222;
    border-bottom: 6px solid #40E583;
}

    .topbar h1 {
        margin: 7px 0 0 10px;
        font-size: 24px;
        color: #eeeeee;
    }

.menugauche {
    position: fixed;
    float: left;
    margin: 70px 0 0 20px;
    width: 15%;
    padding: 6px 0 0 0;
    background-color: #111111;
    border-radius: 4px;
        -moz-box-shadow: 0px 0px 7px 0px #656565;
        -webkit-box-shadow: 0px 0px 7px 0px #656565;
        -o-box-shadow: 0px 0px 7px 0px #656565;
        box-shadow: 0px 0px 7px 0px #656565;
        filter:progid:DXImageTransform.Microsoft.Shadow(color=#656565, Direction=NaN, Strength=7);
}

    .menugauche > ul > li {
        padding-left: 20px;
    }

    .menugauche > ul > li:nth-child(n+2) {
        font-size: 16px;
        color: #40E583;
        line-height: 30px;
        cursor: pointer;
        background-color: #333333;
        list-style: none;
        
    }

    .menugauche > ul > li:first-child {
        background-color: #111111;
        font-size: 18px;
        color: #ffffff;
        line-height: 34px;
        border-bottom: 4px solid #40E583;
    }

    .menugauche > ul > li:hover:nth-child(n+2) {
        color: #333333;
        background-color: #40E583;
    }

::-webkit-scrollbar-track
{
	background-color: #444444;
}

::-webkit-scrollbar
{
	width: 6px;
	background-color: #444444;
}

::-webkit-scrollbar-thumb
{
	background-color: #40E583;
}
</style>
