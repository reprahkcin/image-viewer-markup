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
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue"
import Konva from "konva"

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
      stage.add(layer)

      const imageObj = new Image()
      imageObj.onload = function () {
        const image = new Konva.Image({
          x: 0,
          y: 0,
          image: imageObj,
          width: stage.width(),
          height: stage.height()
        })
        layer.add(image)
        layer.draw()
      }
      imageObj.src = "https://picsum.photos/500/500"

      const brightnessSlider = new Konva.Rect({
        x: stage.width() - 20,
        y: 10,
        width: 10,
        height: stage.height() - 20,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(brightnessSlider)

      const blurSlider = new Konva.Rect({
        x: stage.width() - 10,
        y: 10,
        width: 10,
        height: stage.height() - 20,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(blurSlider)

      // add controls for shifting the image
      const shiftUpButton = new Konva.Circle({
        x: stage.width() / 2,
        y: 20,
        radius: 10,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(shiftUpButton)

      const shiftDownButton = new Konva.Circle({
        x: stage.width() / 2,
        y: stage.height() - 20,
        radius: 10,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(shiftDownButton)

      const shiftLeftButton = new Konva.Circle({
        x: 20,
        y: stage.height() / 2,
        radius: 10,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(shiftLeftButton)

      const shiftRightButton = new Konva.Circle({
        x: stage.width() - 20,
        y: stage.height() / 2,
        radius: 10,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(shiftRightButton)

      const centerButton = new Konva.Circle({
        x: stage.width() / 2,
        y: stage.height() / 2,
        radius: 10,
        fill: "white",
        stroke: "black",
        strokeWidth: 1
      })
      layer.add(centerButton)

      // add event listeners for shifting the image
      shiftUpButton.on("click", function () {
        const currentY = image.y()
        image.y(currentY - 10)
        layer.batchDraw()
      })

      shiftDownButton.on("click", function () {
        const currentY = image.y()
        image.y(currentY + 10)
        layer.batchDraw()
      })

      shiftLeftButton.on("click", function () {
        const currentX = image.x()
        image.x(currentX - 10)
        layer.batchDraw()
      })

      shiftRightButton.on("click", function () {
        const currentX = image.x()
        image.x(currentX + 10)
        layer.batchDraw()
      })

      centerButton.on("click", function () {
        image.position({ x: stage.width() / 2, y: stage.height() / 2 })
        layer.batchDraw()
      })

      layer.draw()
    })

    return {
      displayContainer
    }
  }
}
</script>
