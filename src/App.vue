<template>
    <div id="app">
        <div>
            <img
                class="app-logo"
                src="https://secure.meetupstatic.com/s/img/286374644891845767035/logo/meetup-logo-script-1200x630.png"
                alt="logo"
            />
        </div>
        <app-navigation />
        <router-view />
        <modal v-if="showModal" @close="close" />
        <spinner v-if="showSpinner">Loading...</spinner>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Vuetify from 'vuetify/lib';
import AppNavigation from './lib/navigation/AppNavigation.vue';
import Modal from './lib/modal/Modal.vue';
import Spinner from './lib/spinner/Spinner.vue';
export default Vue.extend({
    components: { AppNavigation, Modal, Spinner },
    name: 'app',
    vuetify: new Vuetify(),
    computed: {
        showModal() {
            return this.$store.state.modalState.showModal;
        },
        showSpinner() {
            return this.$store.state.showSpinner;
        }
    },
    methods: {
        close() {
            this.$store.commit('SET_MODAL_STATE', {
                modalStateType: 'RESET',
                showModal: false,
            });
            if (this.$route.path !== '/') {
                this.$router.push('/');
            }
        },
    },
});
</script>

<style>
#app {
    font-family: Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin: 0 auto;
    max-width: 500px;
}
.app-nav {
    display: flex;
    justify-content: space-between;
}
a {
    text-decoration: none;
    color: inherit;
}
.app-logo {
    width: 100px;
}
ul {
    list-style: none;
}
</style>
