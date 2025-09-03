<template>
    <div>
        <button class="btn btn-primary" type="button" disabled>
            <span class="spinner-border spinner-border-sm" aria-hidden="true"></span>
            <span role="status">{{ title }}...</span>
        </button>
    </div>
</template>

<script>
    export default{
        name: "Saving",
        props: {
            title: String
        }
    }
</script>

<style>

</style>