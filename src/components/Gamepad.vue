<script>
import { WasmBoy } from 'wasmboy';
/*         //WasmBoy.addPlugin(KeyboardInputPlugin());
        WasmBoy.ResponsiveGamepad.addPlugin({
            name: "Test",
            onGetState: () => {
                //alert("play");
                console.log("onGetState");
            }
        }); */
export default {
    data() {
        return {
            upPressed: false,
            downPressed: false,
            leftPressed: false,
            rightPressed: false,
            APressed: false,
            BPressed: false,
            StartPressed: false,
            SelectPressed: false,
        }
    },
    mounted() {
        //WasmBoy.addPlugin(KeyboardInputPlugin());
        WasmBoy.ResponsiveGamepad.addPlugin({
            name: "Test",
            onGetState: () => {
                //alert("play");
                let state = {
                    A: Number(this.APressed),
                    B: Number(this.BPressed),
                    START: Number(this.StartPressed),
                    SELECT: Number(this.SelectPressed),
                    UP: Number(this.upPressed),
                    DOWN: Number(this.downPressed),
                    LEFT: Number(this.leftPressed),
                    RIGHT: Number(this.rightPressed),
                }

                console.log(state);

                return state;
            }
        });
    }
}
</script>

<template>
    <div id="testoverlay">
        
    </div>
</template>

<style>
#testoverlay {
    width: 100vw;
    height: 100vh;
}
</style>