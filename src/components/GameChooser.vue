<script>
export let eventTarget = new EventTarget();

export default {
    data() {
        return {
            romPathInput: "",
        }
    },
    props: {
        romPath: String
    },
    methods: {
        selectGame() {
            eventTarget.dispatchEvent(new CustomEvent("loadgame", { detail: this.romPathInput }));
        }
    }
}
</script>
<template>
    <div>GameChooser</div>
    <form @submit.prevent="selectGame">
    <input type="text" v-model="romPathInput" />
    <input type="submit" />
    </form>
</template>