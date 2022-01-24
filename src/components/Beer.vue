<template>
    <div>
        <h2 class="beer__title">Beer adviser</h2>
        <div v-if="json">
            <p class="text"><span class="key">Brand:</span> {{ json.brand }}</p>
            <p class="text"><span class="key">Name:</span> {{ json.name }}</p>
            <p class="text"><span class="key">Style:</span> {{ json.style }}</p>
            <p class="text"><span class="key">Hop:</span> {{ json.hop }}</p>
            <p class="text"><span class="key">Yeast:</span> {{ json.yeast }}</p>
            <p class="text"><span class="key">Malts:</span> {{ json.malts }}</p>
            <p class="text"><span class="key">IBU:</span> {{ json.ibu }}</p>
            <p class="text"><span class="key">Alcohol:</span> {{ json.alcohol }}</p>
            <p class="text"><span class="key">Blg:</span> {{ json.blg }}</p>
        </div>
        <button class="beer_btn" @click="fetchData">Suggest a beer!</button>
    </div>
</template>

<script>

export default {
    name: "Beer",
    data() {
        return {
            json: null
        }
    },
    methods: {
        fetchData() {
            return fetch("https://random-data-api.com/api/beer/random_beer", {
                method: "get",
            })
                .then(res => res.json())
                .then(data => (this.json = data))
        }
    },
}
</script>