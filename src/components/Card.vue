<script>
export default {
    data() {
        return {

        }
    },
    props: {
        image: String,
        name: String,
        type: String
    }
}
</script>

<template>
    <div>
        <div class="card-y">
            <img :src="image" alt="">
            <div class="card-footer">
                <h4>{{ name }}</h4>
                <span>{{ type }}</span>
            </div>

        </div>
    </div>
</template>


<style lang="scss" scoped>
@use '../assets/scss/style.scss';

.card-y {
    text-align: center;

    border: solid 1px black;
    background-color: #D48F38;

    img {
        width: 100%;
    }

    h4 {
        color: white;
    }


}

.card-footer {
    height: 120px;
    padding: 20px;
}
</style>