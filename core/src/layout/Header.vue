<template>
    <header id="top" class="nq-blue-bg">
        <div class="nq-icon nimiq-logo pull-left" />
        <div class="menu-toggle pull-left" @click="toggleMenu">
            <div class="line" />
            <div class="line" />
            <div class="line" />
            <div class="line" />
        </div>
        <RouterLink to="/login">
            <h1 class="nq-h1 pull-left hidden-xs">
                Nimiq Wallet Manager
            </h1>
            <h1 class="nq-h1 pull-left show-xs">
                NWM
            </h1>
        </RouterLink>
        <!-- {% if user %} -->
        <ul v-if="isProfileLoaded" class="nav pull-right">
            <li>
                <a class="nq-icon settings" href="#">
                    <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd" clip-rule="evenodd"
                              d="M17.6289 7.76248L18.6839 8.13665C19.4726 8.41738 19.9994 9.16402 19.9994 10.0012C19.9994 10.8384 19.4726 11.5851 18.6839 11.8658L17.6289 12.2416C17.3236 12.3503 17.0786 12.5832 16.9547 12.8826C16.8308 13.182 16.8396 13.5199 16.9789 13.8125L17.4589 14.8233C17.8176 15.5797 17.6619 16.48 17.07 17.0719C16.478 17.6639 15.5777 17.8196 14.8214 17.4608L13.8105 16.9808C13.5179 16.8416 13.18 16.8328 12.8806 16.9567C12.5812 17.0806 12.3483 17.3255 12.2397 17.6308L11.8647 18.6858C11.5835 19.4743 10.8368 20.0009 9.99968 20.0009C9.16253 20.0009 8.41584 19.4743 8.13468 18.6858L7.75968 17.6316C7.65144 17.326 7.41864 17.0807 7.11912 16.9566C6.81961 16.8325 6.48151 16.8413 6.18885 16.9808L5.17802 17.4608C4.42164 17.8196 3.52136 17.6639 2.92941 17.0719C2.33745 16.48 2.18175 15.5797 2.54052 14.8233L3.02052 13.8125C3.15978 13.5199 3.16855 13.182 3.04466 12.8826C2.92076 12.5832 2.6758 12.3503 2.37052 12.2416L1.31552 11.8666C0.526779 11.5859 0 10.8393 0 10.0021C0 9.16486 0.526779 8.41821 1.31552 8.13748L2.37052 7.76248C2.67586 7.65366 2.92082 7.4206 3.0447 7.12106C3.16858 6.82152 3.1598 6.48352 3.02052 6.19081L2.54052 5.17998C2.18175 4.4236 2.33745 3.52332 2.92941 2.93137C3.52136 2.33941 4.42164 2.18371 5.17802 2.54248L6.18885 3.02331C6.48158 3.16227 6.81945 3.17078 7.11881 3.04675C7.41816 2.92272 7.65101 2.67774 7.75968 2.37248L8.13468 1.31748C8.41584 0.528944 9.16253 0.00244141 9.99968 0.00244141C10.8368 0.00244141 11.5835 0.528944 11.8647 1.31748L12.2397 2.37165C12.3482 2.67706 12.581 2.92224 12.8803 3.04643C13.1797 3.17063 13.5177 3.16223 13.8105 3.02331L14.8214 2.54248C15.5777 2.18371 16.478 2.33941 17.07 2.93137C17.6619 3.52332 17.8176 4.4236 17.4589 5.17998L16.9789 6.19081C16.8393 6.48348 16.8304 6.82159 16.9543 7.12122C17.0782 7.42084 17.3233 7.65388 17.6289 7.76248ZM6.2987 11.5341C6.9461 13.0055 8.39219 13.9642 9.99953 13.9875C10.5249 13.9983 11.0469 13.9007 11.5329 13.7008C13.5744 12.8516 14.5435 10.5103 13.6995 8.46664C12.8315 6.44409 10.509 5.4827 8.46537 6.29997C6.42386 7.14921 5.45471 9.49046 6.2987 11.5341Z"
                              fill="white"
                        />
                    </svg>
                </a>
                <ul class="submenu nq-card">
                    <li>
                        <RouterLink to="/wallets">
                            Manage wallets
                        </RouterLink>
                    </li>
                    <li>
                        <RouterLink to="/contacts">
                            Manage contacts
                        </RouterLink>
                    </li>
                    <li>
                        <RouterLink to="/settings/user/account">
                            Settings
                        </RouterLink>
                    </li>
                    <li class="spacer" />
                    <li>
                        <a @click="logout">
                            Logout
                        </a>
                    </li>
                </ul>
            </li>
        </ul>
        <!-- {% endif %} -->
        <div class="clearfix" />
    </header>
</template>

<script>
import {mapState, mapGetters, mapActions} from 'vuex'
import {AUTH_LOGOUT} from 'store/actions/auth'
import store from 'store'

export default {
    data() {
        return {
            user: false, // var for if
        }
    },
    computed: mapGetters(['isProfileLoaded']),
    methods: {
        logout: function () {
            //
            store.dispatch(AUTH_LOGOUT).then(() =>{
                this.$router.push('/login')
            })
        },
        toggleMenu: function () {
            store.commit('toggleMenu')
        }
    }
}
</script>

<style  lang="scss">
    @media screen and (max-width: 1024px){
        .nimiq-logo{
            display: none;
        }
        header .menu-toggle{
            display: block;
        }
    }
    header .nq-h1 {
        color: #fff;
    }

    .menu-toggle{
        margin-top: 15px;
        margin-left: 15px;
        display: none;
        cursor: pointer;
        .line{
            width: 36px;
            margin-bottom: 6px;
            background-color: #e9b213; // Old browsers
            background: #e9b213; /* Old browsers */
            background: -moz-linear-gradient(-45deg, #e9b213 0%, #ec991c 100%); /* FF3.6-15 */
            background: -webkit-linear-gradient(-45deg, #e9b213 0%,#ec991c 100%); /* Chrome10-25,Safari5.1-6 */
            background: linear-gradient(135deg, #e9b213 0%,#ec991c 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
            filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#e9b213', endColorstr='#ec991c',GradientType=1 ); /* IE6-9 fallback on horizontal gradient */
            height: 5px;
            //E9B213 left top
            //#EC991C right bottom
        }
    }

    .settings {

        height: 20px;
        width: 20px;
    }
</style>
