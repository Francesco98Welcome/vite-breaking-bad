<script>
export default {
    name: 'cardYuGiOh',
    props: {
        card: Object
    }
}
</script>

<template>
    <div>
        <div>
            <img :src="card.card_images[0].image_url" alt="">
        </div>
        <div class="content">
            <h4>
                {{ card.name }}
            </h4>
            <p>
                {{ card.archetype }}
            </p>
        </div>
    </div>
</template>

<style lang="scss">
img {
    width: 100%;
}

.content {
    margin-top: -4px;
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: #d48f38;
}

h4 {
    text-transform: uppercase;
    padding-top: 10px;
    color: white;
}
</style>