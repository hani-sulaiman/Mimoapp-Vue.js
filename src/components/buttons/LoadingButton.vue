<template>
    <button type="submit" :disabled="isLoading">
        <div class="loader" v-if="isLoading"></div>
        <span v-else>Sign</span>
    </button>
</template>
<script>
export default {
    props: {
        ButtonName: String,
        isLoading: Boolean
    }
}
</script>
<style scoped>
button[type='submit'] {
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.loader {
    width: 40px;
    aspect-ratio: 2;
    --_g: no-repeat radial-gradient(circle closest-side, #ffffff 90%, #ffffff00);
    background:
        var(--_g) 0% 50%,
        var(--_g) 50% 50%,
        var(--_g) 100% 50%;
    background-size: calc(100%/3) 50%;
    animation: l3 1s infinite linear;
}

@keyframes l3 {
    20% {
        background-position: 0% 0%, 50% 50%, 100% 50%
    }

    40% {
        background-position: 0% 100%, 50% 0%, 100% 50%
    }

    60% {
        background-position: 0% 50%, 50% 100%, 100% 0%
    }

    80% {
        background-position: 0% 50%, 50% 50%, 100% 100%
    }
}
</style>