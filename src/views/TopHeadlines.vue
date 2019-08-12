<template>
    <div class="top-headlines">
        <v-layout column align-center>
            <v-card
                    class="mx-auto"
                    max-width="800"
                    tile
            >
                <v-list
                        :three-line="true"
                        :sub-group="true"
                        :nav="true"
                        :avatar="true"
                >
                    <v-subheader>REPORTS</v-subheader>
                    <v-list-item-group color="primary">
                        <v-list-item
                                v-for="article in news_list"
                        >
                            <v-list-item-avatar v-if="avatar">
                                <v-img :src="article.urlToImage"></v-img>
                            </v-list-item-avatar>
                            <v-list-item-content>
                                <v-list-item-title v-html="article.title"></v-list-item-title>
                                <v-list-item-subtitle v-if="twoLine || threeLine" v-html="article.content"></v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list-item-group>
                </v-list>
            </v-card>
        </v-layout>

    </div>
</template>

<script>
    import Vue from 'vue'
    import axios from 'axios'
    import VueAxios from 'vue-axios'

    Vue.use(VueAxios, axios)
    export default {
        name: "TopHeadlines",
        data: () => {
            return{
                threeLine: true,
                subheader: true,
                subGroup: true,
                nav: true,
                avatar: true,
                'news_list': '',
                'msg': 'Hello'
            }
        },
        methods: {
            getNewsList: function () {
                this.axios.get('https://newsapi.org/v2/top-headlines?country=us&apiKey=9ff6a014bc4049b290ceb20d9f4d20b1')
                    .then((response) => {
                        console.log(response.data)
                        this.news_list = response.data.articles
                    })
            }
        },
        computed: {

        },
        mounted(){
            this.getNewsList()
        }
    }
</script>

<style scoped>

</style>