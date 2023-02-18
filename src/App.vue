<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <div class="card">
          <div class="card-header">
            <h1>Image Viewer Markup</h1>
          </div>
          <div class="card-body">
            <div ref="displayContainer"></div>
          </div>
          <div class="card-footer">
            <button class="btn btn-primary" @click="capture">Capture</button>
            <button class="btn btn-secondary" @click="addCircle">Add Circle</button>
            <div class="shift-buttons">
              <button class="btn btn-secondary" @click="shiftUp">Up</button>
              <button class="btn btn-secondary" @click="shiftDown">Down</button>
              <button class="btn btn-secondary" @click="shiftLeft">Left</button>
              <button class="btn btn-secondary" @click="shiftRight">Right</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue"
import Konva from "konva"
import jonatanPie from "@/assets/slides/jonatan-pie.jpg"

export default {
  name: "App",

  setup() {
    const displayContainer = ref(null)

    onMounted(() => {
      const stage = new Konva.Stage({
        container: displayContainer.value,
        width: 500,
        height: 500
      })

      const layer = new Konva.Layer()

      const image = new Konva.Image({
        x: 0,
        y: 0,
        width: 500,
        height: 500
      })

      layer.add(image)

      stage.add(layer)

      const imageObj = new Image()
      imageObj.src = jonatanPie

      imageObj.onload = function () {
        image.image(imageObj)
        layer.batchDraw()
      }
    })

    return {
      displayContainer
    }
  }
}
</script>
