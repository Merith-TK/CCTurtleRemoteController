<template>
  
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useWorldStore } from "../store/useWorld";
import { useWorldViewStore } from "../store/useWorldView";

export default defineComponent({
  setup() {
    const world = useWorldStore();
    const worldView = useWorldViewStore();
    return { world, worldView };
  },
  methods: {
    addKeyboardBindings() {
      document.addEventListener("keydown", this.handleKeyDown);
    },
    handleKeyDown(keyEvent: KeyboardEvent) {
      console.log(keyEvent.key);
      switch(keyEvent.key) {
        case 'w':   this.sendTurtleCmd('return tapi.forward()');   break;
        case 's':   this.sendTurtleCmd('return tapi.back()');      break;
        case 'a':   this.sendTurtleCmd('return tapi.left()');      break;
        case 'd':   this.sendTurtleCmd('return tapi.right()');     break;
        case 'q':   this.sendTurtleCmd('return tapi.down()');      break;
        case 'e':   this.sendTurtleCmd('return tapi.up()');        break;
        case 'u':   this.sendTurtleCmd('return tapi.digUp()');     break;
        case 'j':   this.sendTurtleCmd('return tapi.dig()');       break;
        case 'm':   this.sendTurtleCmd('return tapi.digDown()');   break;
        case 'i':   this.sendTurtleCmd('return tapi.placeUp()');   break;
        case 'k':   this.sendTurtleCmd('return tapi.place()');     break;
        case ',':   this.sendTurtleCmd('return tapi.placeDown()'); break;
        case 'o':   this.sendTurtleCmd('return tapi.dropUp()');    break;
        case 'l':   this.sendTurtleCmd('return tapi.drop()');      break;
        case '.':   this.sendTurtleCmd('return tapi.dropDown()');  break;
        case 'c':   this.sendTurtleCmd('return tapi.craft()');     break;
        case 'r':   this.sendTurtleCmd('return tapi.refuel()');    break;
        case 'Delete': this.clearCmdQueue();                       break;
      }
    },
    sendTurtleCmd(cmd: string) {
      if (this.worldView.selectedTurtleId < 0) return;
      this.world.sendCommand(this.worldView.selectedTurtleId, cmd);
    },
    clearCmdQueue() {
      if (this.worldView.selectedTurtleId < 0) return;
      this.world.clearCommandQueue(this.worldView.selectedTurtleId);
    },
  },
  mounted() {
    this.addKeyboardBindings();
  },
});
</script>
