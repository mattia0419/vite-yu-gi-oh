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
    <div class="card">
        <img :src="image" alt="">
        <h4>{{ name }}</h4>
        <span>{{ type }}</span>
    </div>
</template>


<style lang="scss" scoped>
@use '../assets/scss/style.scss';
</style>