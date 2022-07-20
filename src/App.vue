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
            <a href="#" id="logo">
                <img src="@/assets/prog-1.png" alt="" />
            </a>
            <a href="index">Home</a>
            <a href="nova-noticia">News</a>
            <a href="#contact">Contact</a>
            <input
                type="text"
                name="q"
                id="search"
                class="form-control mr-sm-2"
                placeholder="Pesquisar"
                aria-label="Search"
            />
        </div>
        <h2>Portal de noticias h2</h2>
    </header>
    <router-view />
</template>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
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
    top: 0;
    width: 100%;
}

.navbar a {
    float: right;
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
    margin-top: 30px;
    height: 1500px; /* Used in this example to enable scrolling */
}

#navbar li {
    margin: 0 10px;
    padding: 5px;
}

#logo img {
    /*largura*/
    width: 50px;
}

#search {
    margin: 10px;
    padding: 4px;
    width: 15%;
    margin-left: 1100px;
}
</style>
