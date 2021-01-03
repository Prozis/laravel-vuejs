<template>
    <nav class="navbar navbar-expand-lg navbar-dark  bg-dark ">
        <div class="container">
            <router-link to="/" class="navbar-brand"> Главная </router-link>

            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarText">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item active">
                        <router-link to="/foo" class="nav-link">Перейти к Foo</router-link>

                    </li>
                    <li class="nav-item">
                        <router-link to="/news" class="nav-link">news</router-link>

                    </li>
                    <li class="nav-item">
                        <router-link to="/news" class="nav-link">news</router-link>
                    </li>
                </ul>
                <span class="navbar-text">
                  Navbar text with an inline element
                </span>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
name: "NavBar"
}
</script>

<style scoped>

</style>
