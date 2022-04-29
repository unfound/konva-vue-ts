<script lang="ts" setup>
import { onMounted } from 'vue'
import Konva from 'konva'

onMounted(() => {
    const stage = new Konva.Stage({
        container: 'konva',
        width: Math.min(window.innerWidth, 750),
        height: 750,
    })

    const circle = new Konva.Circle({
        x: stage.width() / 2,
        y: 100,
        radius: 70,
        fill: 'red',
        stroke: 'black',
        strokeWidth: 4,
        draggable: true,
        name: 'circle'
    })

    const layer = new Konva.Layer()
    layer.add(circle)
    stage.add(layer)
    layer.draw()
    const tr = new Konva.Transformer()
    layer.add(tr)

    stage.on('click tap', function (e) {
        if (e.target === stage) {
            tr.nodes([])
            layer.draw()
            return
        }

        if (!e.target.hasName('circle')) {
            return
        }

        // (stage.find('Transformer') as any)?.destroy()
        tr.nodes([e.target])
        layer.draw()
    })
})
</script>

<template>
    <div id="konva"></div>
</template>

<style>
#konva {
    max-width: 750px;
    margin: 0 auto;
    background: #ffe6d1;
}
</style>