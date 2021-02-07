<template>
    <div>
        <p class="homeText">
            Listaa tapahtumia
        </p>
        <br />
        <ul id="notes">
            <li v-for="note in notes" :key="note.id">
                {{ note.content }}. Tärkeä:
                {{ note.important ? "Kyllä" : "Ei" }}
            </li>
        </ul>
    </div>
</template>
<script>
import axios from "axios"
export default {
    name: "ListEvent",
    data() {
        return {
            notes: [],
            error: null,
        }
    },
    async created() {
        try {
            const { data } = await axios.get("http://localhost:3000/notes")
            this.notes = data
        } catch (e) {
            this.error = e
        }
    },
}
</script>
<style scoped>
.homeText {
    font-size: 35px;
    color: red;
    text-align: center;
    position: relative;
    top: 30px;
    text-shadow: 2px 2px 2px gray;
}
</style>
