<script>

export default {
    props: {
        results: Array
    }
}

</script>

<template>
    <div class="list-container">
        <div class="list-item" v-for="result in results" :key="result.id">
                <!-- Currently shows a problem, needed more time to dig into the issue. -->
                <img class="item-image" :src='result.image_url' :alt='result.name' />
            <div class="item-text">
                <h3 class="item-name">{{ result.name }}</h3>
                <p>{{ result.tagline }}</p>
                <!-- Added a scroll here, needs an idicator but I did not want to spend too much time here. -->
                <p class="item-description">{{ result.description }}</p>
                <div class="item-desktop-addons">
                    <div>
                        Pair it with
                        <ul>
                            <!-- Loops through the pairings for each item and lists as bullets -->
                            <li v-for="pairing in result.food_pairing" :key="pairing">
                                {{ pairing }}
                            </li>
                        </ul>
                    </div>
                    <p>ABU: {{ result.abv }} | IBU: {{ result.ibu }} | PH: {{ result.ph }} </p>
                </div>

            </div>
        </div>
    </div>
</template>

<style scoped>
/* Could need a check? I am very new to CSS Grid */
.list-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 1rem;
    grid-auto-rows: minmax(50px, auto);
    align-self: flex-start;
    width: 100vw;
    font-family: 'Open Sans', sans-serif;
    font-size: 16px;
}

.list-item {
    display: flex;
    flex-direction: row;
    max-width: 45vw;
    max-height: 50vh;
}

.item-image {
    max-height: 85%;
    max-width: 15vw;
    padding: 30px;
}

.item-text {
    line-height: 1.5em;
}

.item-name {
    font-family: 'Montserrat', sans-serif;
    font-weight: 700;
    font-size: 20px;
}

.item-description {
    max-height: 20%;
    overflow: scroll;
}

.item-desktop-addons {
    display: flex;
    flex-direction: column;

}

@media only screen and (max-width: 600px) {
    .list-container {
        display: grid;
        grid-template-columns: repeat(1, 1fr);
        grid-gap: 1rem;
        grid-auto-rows: minmax(50px, auto);
        align-self: flex-start;
        width: 90vw;
        font-family: 'Open Sans', sans-serif;
        font-size: 16px;
    }

    .list-item {
        display: flex;
        flex-direction: column;
        max-width: 90vw;
        max-height: fit-content; 
    }

    .item-image {
        height: fit-content;
        transform: rotate(90deg);
    }

    .item-description {
        height: fit-content;
        overflow: visible;
    }

    .item-desktop-addons {
        display: none;

    }

}
</style>
