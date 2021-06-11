<template>
    <div>
        <Main />
    </div>
</template>

<script>
    import Main from './components/Main'

    export default {
        name: 'App',
        components: {
            Main,
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    :root {
        --text-color: #43434f;
        --text-light: 300;
        --text-weight: 400;
        --text-bold: 500;
        --font: 'Rubik', sans-serif;
    }

    body {
        font-family: var(--font);
    }

    .container {
        width: 100%;
        max-width: 1280px;
        margin: 0 auto;
    }

    .display {
        display: block !important;
    }

    @keyframes fadein {
        from {
            opacity: 0;
            -webkit-transform: translate3d(0, -100%, 0);
            transform: translate3d(0, -100%, 0);
        }

        to {
            opacity: 1;
            -webkit-transform: translate3d(0, 0, 0);
            transform: translate3d(0, 0, 0);
        }
    }

    .multiselect-input {
        min-height: 42px;
        font-size: 20px;
        font-weight: var(--text-light);
    }
</style>