<template>
    <section class="home">
        <TheNavbar />
        <section class="home-hero-section">
            <div class="home-hero-inner container has-text-centered">
                <span class="hero-badge home-hero">
                    <span class="badge-dot" />
                    Vue 3 · Built on Bulma
                </span>

                <h1 class="hero-headline home-hero">
                    Lightweight UI Components<br>
                    for <span class="headline-accent">Vue 3</span>
                </h1>

                <p class="hero-sub home-hero">
                    40+ accessible, responsive components based on Bulma.
                    Drop into any Vue 3 project in minutes.
                </p>

                <div class="hero-ctas home-hero">
                    <router-link to="/documentation/start" class="btn-primary">
                        Get Started
                    </router-link>
                    <router-link to="/documentation" class="btn-ghost">
                        Browse Components →
                    </router-link>
                </div>

                <div class="install-block home-hero">
                    <code>npm install buefy</code>
                    <button class="copy-btn" @click="copyInstall">
                        <span v-if="copied">✓ Copied</span>
                        <span v-else>Copy</span>
                    </button>
                </div>

                <div class="hero-gh-buttons home-hero">
                    <iframe
                        src="https://ghbtns.com/github-btn.html?user=buefy&repo=buefy&type=star&count=true&size=large"
                        frameborder="0"
                        scrolling="0"
                        width="160px"
                        height="30px"
                    />
                    <iframe
                        src="https://ghbtns.com/github-btn.html?user=buefy&repo=buefy&type=fork&count=false&size=large"
                        frameborder="0"
                        scrolling="0"
                        width="80px"
                        height="30px"
                    />
                </div>

                <small class="home-hero">v{{ version }}</small>
            </div>
        </section>

        <section class="stats-bar">
            <div class="stat">
                <span class="stat-num">9,500+</span>
                <span class="stat-label">GitHub Stars</span>
            </div>
            <div class="stat-divider" />
            <div class="stat">
                <span class="stat-num">40+</span>
                <span class="stat-label">Components</span>
            </div>
            <div class="stat-divider" />
            <div class="stat">
                <span class="stat-num">1,100+</span>
                <span class="stat-label">GitHub Forks</span>
            </div>
            <div class="stat-divider" />
            <div class="stat">
                <span class="stat-num">Vue 3</span>
                <span class="stat-label">Native Support</span>
            </div>
        </section>

        <section class="features-section">
            <div class="container">
                <div class="features-grid">
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="puzzle-outline" />
                        </div>
                        <h3>Vue 3 Native</h3>
                        <p>Built from the ground up for Vue 3. No Vue 2 compatibility shim, no legacy debt.</p>
                    </div>
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="palette-outline" />
                        </div>
                        <h3>Bulma-Powered</h3>
                        <p>Inherits your entire Bulma theme. CSS variables, SCSS overrides — all supported.</p>
                    </div>
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="lightning-bolt-outline" />
                        </div>
                        <h3>Lightweight</h3>
                        <p>~88KB min+gzip including Bulma. Tree-shake individual components for even less.</p>
                    </div>
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="check-circle-outline" />
                        </div>
                        <h3>Accessible</h3>
                        <p>ARIA labels, keyboard navigation, and focus management built into every component.</p>
                    </div>
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="responsive" />
                        </div>
                        <h3>Responsive</h3>
                        <p>Every component works across mobile, tablet, and desktop without extra configuration.</p>
                    </div>
                    <div class="feature-card features">
                        <div class="card-icon">
                            <b-icon icon="code-braces" />
                        </div>
                        <h3>TypeScript Ready</h3>
                        <p>Full TypeScript definitions included. Autocomplete and type safety out of the box.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="compat-section">
            <div class="container">
                <div class="compat-callout">
                    <b-icon icon="alert-circle-outline" class="callout-icon" />
                    <div>
                        <strong>Vue 3 only.</strong>
                        Buefy v1.x requires Vue 3.0+. Vue 2 support ended with v0.x and will not receive further updates.
                        <a href="https://v2.buefy.org" target="_blank" rel="noopener">View Vue 2 docs →</a>
                    </div>
                </div>
            </div>
        </section>

        <section class="quick-install-section">
            <div class="container has-text-centered">
                <h2 class="section-title">Get started in seconds</h2>
                <p class="section-sub">Install via your preferred package manager</p>
                <div class="install-tabs">
                    <button
                        v-for="tab in installTabs"
                        :key="tab.id"
                        class="tab-pill"
                        :class="{ 'is-active': activeInstallTab === tab.id }"
                        @click="activeInstallTab = tab.id"
                    >
                        {{ tab.label }}
                    </button>
                </div>
                <div class="code-block">
                    <pre><code>{{ currentInstallCmd }}</code></pre>
                    <button class="copy-btn" @click="copyInstallCmd">
                        <span v-if="copiedInstall">✓ Copied</span>
                        <span v-else>Copy</span>
                    </button>
                </div>
            </div>
        </section>

        <section class="component-browser-section">
            <div class="container">
                <h2 class="section-title has-text-centered">40+ Components</h2>
                <p class="section-sub has-text-centered">Everything you need to build modern Vue 3 apps</p>
                <div class="component-browser">
                    <div class="category-row">
                        <div class="category-label">UI / Overlays</div>
                        <div class="chip-row">
                            <router-link to="/documentation/dialog" class="component-chip">Dialog</router-link>
                            <router-link to="/documentation/dropdown" class="component-chip">Dropdown</router-link>
                            <router-link to="/documentation/modal" class="component-chip">Modal</router-link>
                        </div>
                    </div>
                    <div class="category-row">
                        <div class="category-label">Data Display</div>
                        <div class="chip-row">
                            <router-link to="/documentation/carousel" class="component-chip">Carousel</router-link>
                            <router-link to="/documentation/collapse" class="component-chip">Collapse</router-link>
                            <router-link to="/documentation/icon" class="component-chip">Icon</router-link>
                            <router-link to="/documentation/image" class="component-chip">Image</router-link>
                            <router-link to="/documentation/loading" class="component-chip">Loading</router-link>
                            <router-link to="/documentation/message" class="component-chip">Message</router-link>
                            <router-link to="/documentation/notification" class="component-chip">Notification</router-link>
                            <router-link to="/documentation/progress" class="component-chip">Progress</router-link>
                            <router-link to="/documentation/skeleton" class="component-chip">Skeleton</router-link>
                            <router-link to="/documentation/snackbar" class="component-chip">Snackbar</router-link>
                            <router-link to="/documentation/table" class="component-chip">Table</router-link>
                            <router-link to="/documentation/tag" class="component-chip">Tag</router-link>
                            <router-link to="/documentation/toast" class="component-chip">Toast</router-link>
                            <router-link to="/documentation/tooltip" class="component-chip">Tooltip</router-link>
                        </div>
                    </div>
                    <div class="category-row">
                        <div class="category-label">Form Controls</div>
                        <div class="chip-row">
                            <router-link to="/documentation/autocomplete" class="component-chip">Autocomplete</router-link>
                            <router-link to="/documentation/checkbox" class="component-chip">Checkbox</router-link>
                            <router-link to="/documentation/clockpicker" class="component-chip">Clockpicker</router-link>
                            <router-link to="/documentation/colorpicker" class="component-chip">Colorpicker</router-link>
                            <router-link to="/documentation/datepicker" class="component-chip">Datepicker</router-link>
                            <router-link to="/documentation/datetimepicker" class="component-chip">Datetimepicker</router-link>
                            <router-link to="/documentation/field" class="component-chip">Field</router-link>
                            <router-link to="/documentation/input" class="component-chip">Input</router-link>
                            <router-link to="/documentation/numberinput" class="component-chip">Numberinput</router-link>
                            <router-link to="/documentation/radio" class="component-chip">Radio</router-link>
                            <router-link to="/documentation/rate" class="component-chip">Rate</router-link>
                            <router-link to="/documentation/select" class="component-chip">Select</router-link>
                            <router-link to="/documentation/slider" class="component-chip">Slider</router-link>
                            <router-link to="/documentation/switch" class="component-chip">Switch</router-link>
                            <router-link to="/documentation/taginput" class="component-chip">Taginput</router-link>
                            <router-link to="/documentation/timepicker" class="component-chip">Timepicker</router-link>
                            <router-link to="/documentation/upload" class="component-chip">Upload</router-link>
                        </div>
                    </div>
                    <div class="category-row">
                        <div class="category-label">Navigation</div>
                        <div class="chip-row">
                            <router-link to="/documentation/breadcrumb" class="component-chip">Breadcrumb</router-link>
                            <router-link to="/documentation/menu" class="component-chip">Menu</router-link>
                            <router-link to="/documentation/navbar" class="component-chip">Navbar</router-link>
                            <router-link to="/documentation/pagination" class="component-chip">Pagination</router-link>
                            <router-link to="/documentation/sidebar" class="component-chip">Sidebar</router-link>
                            <router-link to="/documentation/steps" class="component-chip">Steps</router-link>
                            <router-link to="/documentation/tabs" class="component-chip">Tabs</router-link>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="home-community-section">
            <div class="container">
                <div v-if="sponsors && sponsors.length" class="community-sponsors">
                    <p class="community-label">Sponsors</p>
                    <div class="community-grid">
                        <div
                            v-for="item in sponsors"
                            :key="item.title"
                            class="community-item"
                        >
                            <a
                                :href="item.url"
                                target="_blank"
                                rel="noopener noreferrer"
                            >
                                <img
                                    class="image-has-shadow"
                                    :src="getSponsorImg(item.img)"
                                    :alt="item.title"
                                />
                            </a>
                            <a
                                class="community-item-title"
                                :href="item.url"
                                target="_blank"
                                rel="noopener noreferrer"
                            >{{ item.title }}</a>
                        </div>
                    </div>
                </div>

                <div class="community-expo">
                    <p class="community-intro">
                        Websites and apps
                        <a class="community-link" @click="tweet">#MadeWithBuefy</a>
                        from the
                        <router-link to="/expo" class="community-link">Expo page</router-link>
                    </p>
                    <div class="community-grid">
                        <div
                            v-for="item in expo"
                            :key="item.title"
                            class="community-item"
                        >
                            <a
                                :href="item.url"
                                target="_blank"
                                rel="noopener noreferrer"
                            >
                                <img
                                    class="image-has-shadow"
                                    :src="getExpoImg(item.img)"
                                    :alt="item.title"
                                />
                            </a>
                            <a
                                class="community-item-title"
                                :href="item.url"
                                target="_blank"
                                rel="noopener noreferrer"
                            >{{ item.title }}</a>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <TheFooter />
    </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import { BIcon } from "buefy";

import TheNavbar from "../components/TheNavbar.vue";
import TheFooter from "../components/TheFooter.vue";
import Package from "../../../../package.json";
import expoData from "@/data/expo";
import sponsorsData from "@/data/sponsors";
export default defineComponent({
    name: "App",
    components: {
        BIcon,
        TheNavbar,
        TheFooter,
    },
    data() {
        return {
            version: Package.version,
            expo: expoData.filter((item) => {
                return item.featured;
            }),
            sponsors: sponsorsData,
            copied: false,
            activeInstallTab: 'npm',
            copiedInstall: false,
            installTabs: [
                { id: 'npm',  label: 'npm',  cmd: 'npm install buefy' },
                { id: 'pnpm', label: 'pnpm', cmd: 'pnpm add buefy' },
                { id: 'yarn', label: 'yarn', cmd: 'yarn add buefy' }
            ]
        };
    },
    computed: {
        currentInstallCmd(): string {
            return this.installTabs.find((t) => t.id === this.activeInstallTab)?.cmd ?? ''
        }
    },
    methods: {
        copyInstall() {
            navigator.clipboard.writeText('npm install buefy').then(() => {
                this.copied = true
                setTimeout(() => { this.copied = false }, 2000)
            })
        },
        copyInstallCmd() {
            navigator.clipboard.writeText(this.currentInstallCmd).then(() => {
                this.copiedInstall = true
                setTimeout(() => { this.copiedInstall = false }, 2000)
            })
        },
        tweet() {
            const width = 575;
            const height = 400;
            const left = (window.screen.width - width) / 2;
            const top = (window.screen.height - height) / 2;
            const url = `https://twitter.com/share?url=${encodeURIComponent(
                document.location.protocol + "//" + document.location.host
            )}&text=My website made with Buefy!&hashtags=madewithbuefy`;
            const opts = `status=1,width=${width},height=${height},top=${top},left=${left}`;

            window.open(url, "", opts);
        },
        getExpoImg(img: string) {
            // require won't work on Vite
            // https://vitejs.dev/guide/assets.html#new-url-url-import-meta-url
            // see also https://stackoverflow.com/a/71514878
            return new URL(`/src/assets/expo/${img}`, import.meta.url).href;
        },
        getSponsorImg(img: string) {
            // require won't work on Vite
            // https://vitejs.dev/guide/assets.html#new-url-url-import-meta-url
            // see also https://stackoverflow.com/a/71514878
            return new URL(`/src/assets/sponsors/${img}`, import.meta.url).href;
        },
    },
    mounted() {
        this.$nextTick(() => {
            const homeHeroElements = document.querySelectorAll('.home-hero');
            const featuresElements = document.querySelectorAll('.features');

            // Add reveal classes with delay
            homeHeroElements.forEach((el, index) => {
                setTimeout(() => {
                    el.classList.add('reveal-animation');
                }, index * 100);
            });

            featuresElements.forEach((el, index) => {
                setTimeout(() => {
                    el.classList.add('reveal-animation');
                }, 500 + index * 200);
            });
        });
    },
});
</script>

<style scoped>
.home-hero, .features {
    opacity: 0;
    transform: translateY(20px);
    transition: transform 0.6s ease-out;
}

.home-hero.reveal-animation, .features.reveal-animation {
    opacity: 1;
    transform: translateY(0);
}
</style>
