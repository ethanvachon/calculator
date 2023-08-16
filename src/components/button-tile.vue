<template>
    <div class="button-tile">
        <div @click="$emit('handleClick')" :style="backgroundColor" class="num-button">
            <p class="m-0" :class="{'operator-sizing':backgroundColor.backgroundColor=='#ff8e00'}">{{state.number}}</p>
        </div>
    </div>
</template>

<script>
import { reactive, computed } from 'vue'
export default {
    name: "buttonTile",
    props: ['color', 'number'],
    setup(props) {
        const state = reactive({
            number: props.number,
        })
        const backgroundColor = computed(() => {
            return {
                backgroundColor: `${props.color}`
            }
        })
        return {
            state,
            backgroundColor,
        }
    }
}
</script>
  
<style scoped>
.button-tile {
    width: 5em;
    height: 5em;
    background-color: inherit;
    padding: 0.25em;
    z-index: 20;
  }

  .num-button {
    height: 100%;
    width: 100%;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    color: white;
    cursor: pointer;
  }

  .num-button:hover {
    filter: brightness(0.85);
  }

  .operator-sizing {
    font-size: 1.4em;
    padding-bottom: 0.2em;
  }
</style>