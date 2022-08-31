<template>
    <div >

      <AppHeader />
  <div class="container">
    <nav>
      <h2>Filters</h2>
    </nav>
    <h5>Shapes</h5>
    <button
      @click="selectShape(shape)"
      v-for="shape in shapes"
      :key="shape"
      class="shape"
      :class="{ selected: activeShapes.includes(shape) }"
    >
      {{ shape }}
    </button>

    <h5>Colors</h5>
    <button
      class="color"
      :class="{
        selected: activeColors.includes(color),
      }"
      :style="{ backgroundColor: color }"
      @click="selectColor(color)"
      v-for="color in colors"
      :key="color"
    ></button>

    <h5 class="wording">
      {{ wording }} items: ({{ activeShapes.length * activeColors.length }})
    </h5>

    <div class="items">
      <template v-for="shape in activeShapes">
        <div v-for="color in activeColors" class="item-container">
          <div
            class="item"
            :style="{ backgroundColor: color, clipPath: shapeStyleMap[shape] }"
          />
        </div>
      </template>
    </div>
  </div>
</div>
</template>

<script>
import { ref, computed } from "vue";
import AppHeader from '../../components/AppHeader';
export default {
  head() {
    return {
      title: "Home",
    };
  },
  components: {
      AppHeader
  },
  setup() {
    const selectedShapes = ref([shapes[0]]);
    const selectedColors = ref([]);
    const selectColor = (color) => {
      const colorIndex = selectedColors.value.indexOf(color);
      if (colorIndex < 0) selectedColors.value.push(color);
      else selectedColors.value.splice(colorIndex, 1);
    };
    const selectShape = (shape) => {
      const shapeIndex = selectedShapes.value.indexOf(shape);
      if (shapeIndex < 0) selectedShapes.value.push(shape);
      else selectedShapes.value.splice(shapeIndex, 1);
    };
    const activeColors = computed(() =>
      selectedColors.value.length ? selectedColors.value : colors
    );
    const activeShapes = computed(() =>
      selectedShapes.value.length ? selectedShapes.value : shapes
    );
    const wording = computed(() => {
      const activeS = activeShapes.value;
      const activeC = activeColors.value;
      const allShapesSelected = activeS.length === shapes.length;
      const allColorsSelected = activeC.length === colors.length;
      if (allShapesSelected && allColorsSelected) {
        return "All";
      }
      if (activeC.length === 1) {
        if (allShapesSelected) {
          return `All ${activeC[0]}`;
        }
        if (activeS.length === 1) {
          return `${activeC[0]} ${activeS[0]}`;
        }
        return `Multiple ${activeC[0]}`;
      }
      if (activeS.length === 1) {
        if (allColorsSelected) {
          return `All ${activeS[0]}`;
        }
        if (activeC.length === 1) {
          return `${activeC[0]} ${activeS[0]}`;
        }
        return `Multiple ${activeS[0]}`;
      }
      return "Multiple";
    });
    return {
      shapes,
      colors,
      shapeStyleMap,
      activeColors,
      activeShapes,
      selectColor,
      selectShape,
      wording,
    };
  },
};

// defining shapes
const shapes = ["round", "oval", "triangle", "rectangle"];
// defining colors
const colors = ["red", "blue", "green", "yellow", "lightblue", "gray"];
const shapeStyleMap = {
  oval: "ellipse(25% 40% at 50% 50%)",
  round: "circle(50% at 50% 50%)",
  triangle: "polygon(50% 0%, 0% 100%, 100% 100%)",
  rectangle: "inset(5% 20% 15% 10%)",
};
</script>

<style>
  .main {
    margin: 30px
}
.container {
  background-color: #efefef;
  padding: 10px 30px;
}

button {
  cursor: pointer;
  margin-right: 0.5rem;
}

.shape {
  background: white;
  border: 1px solid grey;
  border-radius: 8px;
  text-transform: capitalize;
  font-size: 0.75rem;
}
.shape.selected {
  background: #d5d6f3;
}
.color {
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.5);
  border: none;
}
.color.selected {
  border: 1px solid grey;
}

.wording:first-letter {
  text-transform: uppercase;
}

.items {
  display: grid;
  gap: 2rem;
}
@media (min-width: 680px) {
  .items {
    grid-template-columns: repeat(3, auto);
  }
}
.item-container {
  background-color: white;
  padding: 10px;
  display: grid;
  place-items: center;
}
.item {
  width: 100px;
  height: 100px;
  clip-path: v-bind(shapeStyleMap[currentShape]);
}
</style>
