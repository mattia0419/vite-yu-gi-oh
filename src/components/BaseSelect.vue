<script>
export default {
    data() {
        return {
            selectedData: ''
        }
    },
    props: {
        data: Array
    },
    emits: ['change-selection'],
}
</script>


<template>
    <select v-model="selectedData" @change="$emit('change-selection', selectedData)">
        <option value="" selected>seleziona un valore</option>
        <option v-for='option in data' :value="option">{{ option }}</option>
    </select>
</template>


<style lang="scss" scoped></style>