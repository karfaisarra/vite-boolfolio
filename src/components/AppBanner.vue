<script>
export default {
    name: 'AppBanner',
    props: {
        title: String
    }
}
</script>

<template>
    <div class="banner shadow-lg">
        <h1 class="py-4 text-uppercase text-center"> &lt; {{ title }} &#47;&gt;</h1>
    </div>

</template>

<style lang="scss" scoped>
.banner {
    background-color: #396544;
    color: white;
    margin-bottom: -0.5rem;
}
</style>