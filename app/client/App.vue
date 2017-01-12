<template>
    <div>
        <history></history>
        <chat></chat>
        <login></login>
    </div>
</template>

<script>
import history from './components/history.vue';
import chat from './components/chat.vue';
import login from './components/login.vue';

export default {
    name: 'app',
    data() {
        return {
            unLogin: true,
        }
    },
    created() {
        window.socket = io.connect(); //与服务器进行连接
    },
    components: {
        history,
        chat,
        login,
    }
}
</script>

<style>
html,body {
    height: 100%;
}
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif, 'Micorsoft YaHei';
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

h1, h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

p {
    line-height: 1.5;
    margin: 0;
}
</style>
