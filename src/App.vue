<template>
    <head>
        <!--FONTE DE ICONES CDNJ-->
        <link
            rel="stylesheet"
            href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css"
            integrity="sha512-KfkfwYDsLkIlwQp6LFnl8zNdLGxu9YAA1QvwINks4PhcElQSvqcyVLLD9aMhXd13uQjoXtEKNosOWaZqXgel0g=="
            crossorigin="anonymous"
            referrerpolicy="no-referrer"
        />
    </head>
    <header>
        
        <div class="navbar">
            <div class="logo-container">
                <a href="/">
                    <img id="logo" src="@/assets/prog-1.png" alt="" />
                </a>
                <a href="/">
                    <div id="text-logo">Udi City Times</div>
                </a>
            </div>
            <div class="right-buttons">
                
    
                
                <a href="/">Feed</a>
                <a href="nova-noticia">Nova noticia</a>
            </div>
            
            <!-- <a href="#contact" :disabled='true' >Contact</a> -->
        </div>
    </header>
    
    <div class="main">
        <router-view />
    </div>
</template>

<style>
#app {
    font-family: 'Times New Roman', Times, serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}


nav {
    padding: 30px;
}

nav a {
    font-weight: bold;
    color: #2c3e50;
}

nav a.router-link-exact-active {
    color: #42b983;
}
body {
    margin: 0;
}

.navbar {
    overflow: hidden;
    background-color: #333;
    position: fixed;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: right;
    top: 0;
    width: 100%;
}

.navbar a {
    display: block;
    color: #f2f2f2;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: 17px;
}

.navbar a:hover {
    background: #ddd;
    color: black;
}

.main {
    padding: 16px;
    margin-top: 80px;
    /* height: 3000px; Used in this example to enable scrolling */
}

#navbar li {
    margin: 0 10px;
    padding: 5px;
}

#logo {
    /*largura*/
    width: 50px;
    height: 50px;
}

.right-buttons{
    display: flex;
    flex-direction: row;
    align-items: center;
}
.logo-container{
    display: flex;
    width: 100%;
}
.logo-container a{
    padding: 0px;
}
#text-logo{
    color: #f2f2f2;
    font-size: 32px;
    padding: 10px;
}
#search {
    margin: 10px;
    padding: 4px;
    width: 15%;
}


</style>
