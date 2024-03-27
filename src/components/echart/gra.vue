<template>
    <div>
        <div id="main" style="width:100%;height:6.0rem;"></div>
    </div>
</template>

<script>
import * as echarts from 'echarts';
import echartMixins from "@/utils/resizeMixins";
export default {
    data() {
        return {
        };
    },
    mixins: [echartMixins],
    mounted() {
        this.draw();

    },
    methods: {
        draw() {
            // 基于准备好的dom，初始化echarts实例
            this.chart = this.$echarts.init(document.getElementById("main"));
            var chartDom = document.getElementById('main');
            var myChart = echarts.init(chartDom);
            var option;

            const data = [
                {
                    fixed: true,
                    x: myChart.getWidth() / 2,
                    y: myChart.getHeight() / 2,
                    symbolSize: 20,
                    id: '-1'
                }
            ];
            const edges = [];
            option = {
                series: [
                    {
                        type: 'graph',
                        layout: 'force',
                        animation: false,
                        data: data,
                        force: {
                            // initLayout: 'circular'
                            // gravity: 0
                            repulsion: 100,
                            edgeLength: 5
                        },
                        edges: edges
                    }
                ]
            };


            setInterval(function () {
                data.push({
                    id: data.length + ''
                });
                var source = Math.round((data.length - 1) * Math.random());
                var target = Math.round((data.length - 1) * Math.random());
                if (source !== target) {
                    edges.push({
                        source: source,
                        target: target
                    });
                }
                myChart.setOption({
                    series: [
                        {
                            roam: true,
                            data: data,
                            edges: edges
                        }
                    ]
                });
                // console.log('nodes: ' + data.length);
                // console.log('links: ' + data.length);
            }, 200);

            option && myChart.setOption(option);
        },
        destroyed() {
            window.onresize = null;
        }
    }
};
</script>

<style scoped></style>