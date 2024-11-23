<script>
import NavbarLink from './NavbarLink.vue';

export default {
    components: {
        NavbarLink
    },
    created() {
        this.getThemeSetting();
    },
    computed: {
        publishedPages() {
            return this.pages.filter(p => p.published)
        }
    },
    props:['pages', 'activePage', 'navLinkClick' ],
    data() {
            return {
                theme: 'light',
            }
        },
        methods: {
            changeTheme() {
                let theme = 'light';

                if(this.theme == 'light'){
                    theme = 'dark';
                }
                this.theme = theme;
                this.storeThemeSetting();
            },
            storeThemeSetting() {
                localStorage.setItem('theme', this.theme);
            },
            getThemeSetting() {
                let theme = localStorage.getItem('theme');
                console.log(theme)
    
                if (theme) {
                    this.theme = theme;
                }
            }
        }
}
</script>

<template>
    <nav class="main-navbar">
        <div>
            <a href="#" class="">Ceramica</a>
            <ul class="">
                <li v-for="(page, index) in Pages" class="nav-item" :key="index">
                    <navbar-link
                    :page="page"
                    :isActive="activePage == index"
                    @click.prevent="navLinkClick(index)"
                    ></navbar-link>
                </li>
            </ul>
        </div>
    </nav>
</template>