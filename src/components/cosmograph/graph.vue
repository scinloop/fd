<template>
    <div ref="cosmographContainer" style="width: 10%; height: 500px;"></div>
</template>

<script>
import { Cosmograph } from '@cosmograph/cosmograph';
export default {
    name: 'CosmographComponent',
    data() {
        return {
            nodes: [
                { id: '1', color: '#88C6FF' },
                { id: '2', color: '#FF99D2' },
                { id: '3', color: [227, 17, 108, 1] }, // Faster than providing a hex value
            ],
            links: [
                { source: '1', target: '2' },
                { source: '1', target: '3' },
                { source: '2', target: '3' },
            ]
        }
    },
    mounted() {
        // 创建 HTML 元素的引用
        const targetElement = this.$refs.cosmographContainer

        // 定义配置
        const config = {
            nodeColor: d => d.color,
            nodeSize: 20,
            linkWidth: 2,
            // 其他配置...
        }

        // 创建 Cosmograph 实例
        const cosmograph = new Cosmograph(targetElement, config)
        cosmograph.setData(this.nodes, this.links)
    }
}
</script>