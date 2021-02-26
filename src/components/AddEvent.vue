<template>
    <div>
        <p class="homeText">Syötä tapahtuma</p>
        <br />
        <form @submit.prevent="postEvent">
            Tapahtuman nimi:
            <input type="text" v-model="event" />
            Tärkeä?
            <input type="checkbox" v-model="important" />
            <br />
            <button type="postEvent">Lähetä</button>
        </form>
        <div v-if="success">
            {{ success }}
        </div>
        <div v-if="error">
            {{ error }}
        </div>
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
            success: false,
        }
    },
    methods: {
        async postEvent() {
            try {
                if (this.event === "") {
                    throw "Tapahtuman nimi ei voi olla tyhjä"
                } else {
                    await axios.post("http://localhost:3000/notes", {
                        content: this.event,
                        important: this.important,
                    })
                    this.event = ""
                    this.important = false

                    this.success = "Tietojen lähetys onnistui"
                    // timeout and set success back to false
                }
            } catch (e) {
                console.log(e)
                // handle axios error
                this.error = e
            }
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
