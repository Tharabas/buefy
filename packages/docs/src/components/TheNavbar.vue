<template>
    <nav
        class="navbar docs-navbar is-spaced has-shadow"
        :class="{ 'is-primary is-transparent': isLight, 'is-scrolled': isScrolled }"
    >
        <div class="container">
            <div class="navbar-brand">
                <router-link
                    to="/"
                    class="navbar-item"
                    title="Buefy: lightweight UI components for Vue.js based on Bulma"
                    active-class=""
                >
                    <img
                        v-if="isLight"
                        src="../assets/buefy-light.png"
                        alt="Buefy"
                    >
                    <img
                        v-else
                        src="../assets/buefy.png"
                        alt="Buefy"
                    >
                </router-link>

                <a
                    class="navbar-item"
                    href="https://github.com/buefy/buefy"
                    target="_blank"
                    title="Github"
                >
                    <b-icon icon="github" />
                </a>

                <a
                    class="navbar-item"
                    href="https://discord.buefy.org/"
                    target="_blank"
                    title="Discord"
                >
                    <b-icon icon="discord" />
                </a>

                <a
                    class="navbar-item"
                    href="https://x.com/buefycss"
                    target="_blank"
                    title="Twitter"
                >
                    <b-icon
                        pack="fa"
                        custom-class="fa-brands"
                        icon="x-twitter"
                    />
                </a>

                <span
                    class="navbar-burger burger"
                    :class="{ 'is-active': isMenuActive }"
                    @click="isMenuActive = !isMenuActive"
                >
                    <span />
                    <span />
                    <span />
                    <span />
                </span>
            </div>

            <div class="navbar-menu" :class="{ 'is-active': isMenuActive }">
                <div class="navbar-end">
                    <router-link
                        to="/"
                        exact
                        class="navbar-item"
                    >
                        Home
                    </router-link>

                    <router-link to="/documentation" class="navbar-item">
                        Documentation
                    </router-link>

                    <router-link to="/extensions" class="navbar-item">
                        Extensions
                    </router-link>

                    <router-link to="/expo" class="navbar-item">
                        Expo
                    </router-link>

                    <div class="navbar-item has-dropdown is-hoverable">
                        <div class="navbar-link">
                            Info
                        </div>

                        <div class="navbar-dropdown">
                            <strong class="navbar-item is-version">
                                <span class="has-text-primary">Buefy version</span>
                                <span class="has-text-grey">{{ version }}</span>
                            </strong>
                            <strong class="navbar-item is-version">
                                <span class="has-text-bulma">Bulma version</span>
                                <span class="has-text-grey">{{
                                    bulmaVersion
                                }}</span>
                            </strong>

                            <hr class="navbar-divider">
                            <div class="navbar-item">
                                <a
                                    href="https://github.com/buefy/buefy/releases"
                                    target="_blank"
                                    rel="noopener"
                                >
                                    Changelogs
                                </a>
                            </div>
                        </div>
                    </div>

                    <div class="navbar-item">
                        <router-link
                            to="/documentation/start"
                            class="navbar-cta"
                        >
                            Get Started
                        </router-link>
                    </div>

                    <div class="navbar-item">
                        <ThemeToggle />
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import { BIcon } from 'buefy'
import ThemeToggle from '@/components/ThemeToggle.vue'

import buefyPackage from '../../../../package.json'
import bulmaPackage from 'bulma/package.json'
import { useTheme } from '@/composables/useTheme'

export default defineComponent({
    components: { BIcon, ThemeToggle },
    data() {
        return {
            isMenuActive: false,
            isScrolled: false,
            isLight: useTheme().isLight,
            version: buefyPackage.version,
            bulmaVersion: bulmaPackage.version
        }
    },
    methods: {
        closeMenu() {
            this.isMenuActive = false
        }
    },
    mounted() {
        this.$eventHub.on('navigate', this.closeMenu)
        this._onScroll = () => { this.isScrolled = window.scrollY > 60 }
        window.addEventListener('scroll', this._onScroll, { passive: true })
        useTheme().setTheme(useTheme().getTheme())
    },

    beforeUnmount() {
        this.$eventHub.off('navigate', this.closeMenu)
        window.removeEventListener('scroll', this._onScroll)
        document.documentElement.classList.remove('is-clipped-touch')
    }
})
</script>
