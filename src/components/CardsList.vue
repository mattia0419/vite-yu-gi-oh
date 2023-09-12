<script>
import Card from './Card.vue';
import axios from 'axios';

export default {
    data() {
        return {
            cards: [],
        }
    },

    methods: {
        fetchCards() {
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php').then((response) => {
                this.cards = response.data.data;
                console.log(this.cards);


            })
        }
    },
    created() {
        this.fetchCards();
    },
    components: {
        Card
    }
}

</script>

<template>
    <div>
        <div class="row  row-cols-2 row-cols-md-3 row-cols-lg-4">

            <Card v-for="card in cards" :name="card.name" :type="card.archetype"
                :image="card.card_images[0].image_url_cropped" class="col bg-orange g-4"></Card>

        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../assets/scss/style.scss';

.bg-orange {
    background-color: #D48F38;
}
</style>