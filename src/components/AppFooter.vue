<script>
export default {
    name: 'AppFooter',
}
</script>
<template>
    <footer>
        <div class="container">
            <div class="row">
                <div class="col"></div>
                <div class="col text-end">
                    <a class="my_btn btn " href="https://github.com/karfaisarra">GitHub</a>
                </div>
            </div>
        </div>
    </footer>

</template>

<style lang="scss" scoped>
.my_btn {
    color: #396544;
    font-weight: bold;

    &:hover {
        color: white;
    }
}
</style>