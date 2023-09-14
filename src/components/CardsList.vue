<script>
import Card from './Card.vue';
import axios from 'axios';
import BaseSelect from './BaseSelect.vue';
export default {
    data() {
        return {
            cards: [],
            activePage: 0,
            apiUri: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=',
            archeTypes: [],
            apiUriArchetypes: 'https://db.ygoprodeck.com/api/v7/archetypes.php',
            type: '',
            uriCardsFilter: 'https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype='
        }
    },

    methods: {
        fetchCards(endPoint) {
            axios.get(endPoint).then((response) => {
                this.cards = response.data.data;
                console.log(this.cards);
            })
        },
        fetchArchetypes(endPoint) {
            axios.get(endPoint).then((response) => {
                for (let i = 0; i < 10; i++) {
                    this.archeTypes.push(response.data[i].archetype_name);
                    console.log(this.archeTypes);
                }



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

        },
        filterCards(term) {
            console.log('app ha ricevuto' + term);
            this.fetchCards(this.uriCardsFilter + term)
        }
    },
    created() {
        this.fetchCards(this.apiUri);
        this.fetchArchetypes(this.apiUriArchetypes);
    },
    components: {
        Card,
        BaseSelect
    }

}
</script>

<template>
    <div>
        <BaseSelect :data="archeTypes" @change-selection="filterCards"></BaseSelect>
        <button class="btn btn-primary m-3" @click="prev()">Prev</button>
        <button class="btn btn-primary m-3" @click="next()">Next</button>
        <div class="row g-4 row-cols-2 row-cols-md-3 row-cols-lg-4">

            <Card v-for="card in cards" :name="card.name" :type="card.archetype"
                :image="card.card_images[0].image_url_cropped" class="col bg-orange"></Card>

        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../assets/scss/style.scss';
</style>