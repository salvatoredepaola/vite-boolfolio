<script>
export default {
    name: "ErrorPage",
    data() {
        return {

        }
    }
}
</script>

<template>

    <section>
        <h1>Not Found {{ $route.params.code }}</h1>
        <p>Errore</p>
    </section>

</template>

<style>

</style>