<template>
    <div>
        <p class="homeText">
            Syötä tapahtuma
        </p>
        <br />
        <form @submit.prevent="postEvent">
            Tapahtuman nimi:
            <input type="text" v-model="event" />
            Tärkeä?
            <input type="checkbox" v-model="important" />
            <br />
            <button type="postEvent">
                Lähetä
            </button>
        </form>
        <ul v-if="error && error.message">
            {{
                error.message
            }}
        </ul>
    </div>
</template>
<script>
import axios from "axios"
export default {
    name: "AddEvent",
    data() {
        return {
            event: "",
            important: false,
            error: null,
        }
    },
    methods: {
        async postEvent() {
            await axios.post("http://localhost:3000/notes", {
                content: this.event,
                important: this.important,
            })
        },
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
