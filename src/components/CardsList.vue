<script>
import Card from './Card.vue';
import axios from 'axios';

export default {
    data() {
        return {
            cards: [],
            activePage: 0,
            apiUri: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=',

        }
    },

    methods: {
        fetchCards(endPoint) {
            axios.get(endPoint).then((response) => {
                this.cards = response.data.data;
                console.log(this.cards);
            })
        },
        next() {

            const nextPage = this.activePage + 20;
            this.activePage = nextPage;
            console.log(this.activePage);
            this.fetchCards(this.apiUri + this.activePage);
        },
        prev() {
            if (this.activePage != 0) {
                const prevPage = this.activePage - 20;
                this.activePage = prevPage;
                console.log(this.activePage);
                this.fetchCards(this.apiUri + this.activePage);
            }
            else {
                return;
            }

        }
    },
    created() {
        this.fetchCards(this.apiUri);
    },
    components: {
        Card
    }

}
</script>

<template>
    <div>
        <button class="btn btn-primary m-3" @click="prev()">Prev</button>
        <button class="btn btn-primary m-3" @click="next()">Next</button>
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">

            <Card v-for="card in cards" :name="card.name" :type="card.archetype"
                :image="card.card_images[0].image_url_small" class="col bg-orange"></Card>

        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../assets/scss/style.scss';
</style>