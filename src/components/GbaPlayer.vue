<script setup>
import { WasmBoy } from 'wasmboy';
import { eventTarget } from './GameChooser.vue';
import Gamepad from './Gamepad.vue';
</script>

<script>
export default {
    data() {
        return {
            ctx: null,
            gba: null,
            inputBuffer: {}
        };
    },
    props: {
        romName: String
    },
    methods: {
    //getControllerState()
    },
    mounted() {
        console.log(WasmBoy);
        const canvas = document.querySelector("#screen");
        WasmBoy.setCanvas(canvas);
        /*        WasmBoy.setJoypadState(controllerState.UP ? 1 : 0,
                    controllerState.RIGHT ? 1 : 0,
                    controllerState.DOWN ? 1 : 0,
                    controllerState.LEFT ? 1 : 0,
                    controllerState.A ? 1 : 0,
                    controllerState.B ? 1 : 0,
                    controllerState.SELECT ? 1 : 0,
                    controllerState.START ? 1 : 0)*/
        WasmBoy.loadROM("/" + this.romName + ".gb");
        setTimeout(() => {
            WasmBoy.play();
        }, 1000);
        window.addEventListener("keydown", (ev) => {
            console.log(ev);
            this.inputBuffer[ev.key] = Date.now();
        });
        window.addEventListener("keyup", (ev) => {
            delete this.inputBuffer[ev.key];
        });
        eventTarget.addEventListener("loadgame", (ev) => {
            WasmBoy.reset();
        });
    },
    components: { Gamepad }
}
</script>

<template>
    <div class="center game-display">
        <canvas id="screen"></canvas>
        <Gamepad class="absolute"></Gamepad>
    </div>
</template>

<style>
#screen {
    border: 1px solid white;
}
</style>

<style scoped>
.game-display {
    height: 100vh;
    position: relative;
}
.absolute {
    
}

.game-display .absolute {
    position: absolute;
    top: 0;
}
</style>