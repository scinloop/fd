<template>
  <div>
    <div class="app" style="height:800px">
      <canvas />
    </div>

    <div class="actions">
      <div class="actions-header">Actions:</div>
      <div class="action" id="pause" @click="togglePause">{{ pauseText }}</div>
      <div class="action" id="fit-view" @click="fitView">Fit View</div>
      <div class="action" id="zoom" @click="zoomIn">Zoom to a point</div>
      <div class="action" id="select-point" @click="selectPoint">Select a point</div>
      <div class="action" id="select-points-in-area" @click="selectPointsInArea">
        Select points in a rectangular area
      </div>
    </div>
  </div>
</template>

<script>
import { nodes, links } from "./data-gen";
import { Graph } from "@cosmograph/cosmos";
export default {
  data() {
    return {
      graph: null,
      canvas: null,
      config: {
        backgroundColor: "#151515",
        nodeSize: 4,
        nodeColor: "#4B5BBF",
        nodeGreyoutOpacity: 0.1,
        linkWidth: 0.1,
        linkColor: "#5F74C2",
        linkArrows: false,
        linkGreyoutOpacity: 0,
        curvedLinks: true,
        renderHoveredNodeRing: true,
        hoveredNodeRingColor: "#4B5BBF",
        simulation: {
          linkDistance: 1,
          linkSpring: 2,
          repulsion: 0.2,
          gravity: 0.1,
          decay: 100000
        },
        events: {

        }
      },
      isPaused: false,
      pauseText: "Pause"
    };
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      const canvas = document.querySelector("canvas");
      this.canvas = canvas
      this.config.events.onClick = (node, i, pos, event) => {
        console.log({ pos })
        console.log({ event })
        if (node && i !== undefined) {
          this.graph.selectNodeByIndex(i);
          this.graph.zoomToNodeByIndex(i);
        } else {
          this.graph.unselectNodes();
        }
        console.log("Clicked node: ", node);
      }
      this.graph = new Graph(canvas, this.config);
      this.graph.setData(nodes, links);
      this.graph.zoom(0.9);
    },
    pause() {
      this.isPaused = true;
      this.pauseText = "Start";
      this.graph.pause();
    },
    start() {
      this.isPaused = false;
      this.pauseText = "Pause";
      this.graph.start();
    },
    togglePause() {
      if (this.isPaused) this.start();
      else this.pause();
    },
    getRandomNodeId() {
      return nodes[Math.floor(Math.random() * nodes.length)].id;
    },
    getRandomInRange([min, max]) {
      return Math.random() * (max - min) + min;
    },
    fitView() {
      this.graph.fitView();
    },
    zoomIn() {
      const nodeId = this.getRandomNodeId();
      this.graph.zoomToNodeById(nodeId);
      this.graph.selectNodeById(nodeId);
      this.pause();
    },
    selectPoint() {
      const nodeId = this.getRandomNodeId();
      this.graph.selectNodeById(nodeId);
      this.graph.fitView();
      this.pause();
    },
    selectPointsInArea() {
      const w = this.canvas.clientWidth;
      const h = this.canvas.clientHeight;
      const left = this.getRandomInRange([w / 4, w / 2]);
      const right = this.getRandomInRange([left, (w * 3) / 4]);
      const top = this.getRandomInRange([h / 4, h / 2]);
      const bottom = this.getRandomInRange([top, (h * 3) / 4]);
      this.pause();
      this.graph.selectNodesInRange([
        [left, top],
        [right, bottom]
      ]);
    }
  }
}
</script>

<style lang="scss">
@import "../assets/scss/demo.scss";
</style>
