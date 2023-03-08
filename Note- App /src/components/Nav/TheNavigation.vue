<template>
    <header>
        <div id="app" >
            <nav id="startchange"
                class="navbar fixed-top navbar-expand-lg navbar-dark navbar-fixed-top scrolled scrolling-navbar navbar-section"
>
                <div class="container-fluid">

                    <!-- Brand -->
                    <a class="navbar-brand" href="/">
                        <strong>Note App</strong>
                    </a>
                    <!-- Collapse -->
                    <button class="navbar-toggler" id="navbar-toggler" type="button" data-toggle="collapse"
                        data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                        aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>

                    <!-- Links -->
                    <div class="collapse navbar-collapse" id="navbarSupportedContent">

                        <!-- Left -->
                        <ul class="navbar-nav mr-auto">

                        </ul>

                        <!-- Right -->
                        <ul class="navbar-nav ml-auto">
                            <li class="nav-item">
                                <span class="nav-link" :class="active" @click="setActivePage('saved-notes')">Saved Notes</span>
                            </li>
                            <li class="nav-item">
                                <span class="nav-link" @click="setActivePage('add-notes')">Add Notes</span>
                            </li>
                        </ul>
                    </div>

                </div>
            </nav>


        </div>
        <nav id="startchange" class="navbar  navbar-expand-lg navbar-dark  navbar-section " style="z-index: 25;">
            <div class="container">
                <!-- Brand -->
                <a class="navbar-brand" href="/">
                    <strong>Note App</strong>
                </a>

                <!-- Links -->
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <!-- Left -->
                    <ul class="navbar-nav mr-auto">
                    </ul>
                    <!-- Right -->
                    <ul class="navbar-nav ml-auto">
                        <li class="nav-item">

                            <span class="nav-link" @click.stop="setActivePage('saved-notes')">Saved Notes</span>
                        </li>
                        <li class="nav-item">
                            <span class="nav-link" @click="setActivePage('add-notes')">Add Notes</span>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>

</template>

<script>

export default {
    emits: ['set-page'],
    methods: {
        setActivePage(page) {
            this.$emit('set-page', page);
        },
    },
}
</script>


<style scoped>

.navbar {
    background: black;
    margin-bottom: 50px;
}


.page-footer,
.top-nav-collapse {
    background-color: black !important;
}

.nav-item .nav-link {
    color: white !important;
    font-family: 'Cormorant', raleway;
    font-weight: 500;
    text-transform: uppercase;
    font-size: 15px;
}

.nav-item .nav-link:hover {
    background-color: #202020;
}

@media only screen and (max-width: 600px) {
    .navbar {
        overflow: hidden;
        padding: 10px 20px 10px 20px ;
    }
}

</style>