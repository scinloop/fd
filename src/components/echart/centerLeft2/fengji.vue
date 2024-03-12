<template>
    <div>
        <el-popover ref="popover" placement="top-start" width="200" trigger="hover" title="wowo" content="风机122121212">
        </el-popover>
        <div v-popover:popover class="windmill">
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
        </div>
        <div class="center"><img src="../../../assets/center.png"></div>
        <div class="body"><img src="../../../assets/body.png"></div>
    </div>
</template>

<script>
export default {
    mounted() {
        let wm = this.$el.querySelector(".windmill");
        let s = 3;
        let a = 3;
        let lf = this.$el.getElementsByClassName('leaf');

        function setup() {
            wm.style.animationDuration = s + "s";
            lf[0].style.display = "block";
            for (let i = 1; i < a; i++) {
                lf[i].style.transform = "rotate(" + (360 / a) * i + "deg)";
                lf[i].style.display = "block";
            }
            for (let i = a; i < 8; i++) {
                lf[i].style.display = "none";
            }
        }

        setup();
    },
};
</script>

<style lang="scss">
* {
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
}

body {
    background-color: black;
}

button {
    background-color: #fff;
}

.windmill {
    width: 77.6px;
    height: 77.6px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -38.8px 0 0 -38.8px;
    animation-name: rotate;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
    z-index: 3;
}

.leaf {
    width: 12.6px;
    height: 38.8px;
    position: absolute;
    top: 0;
    left: 50%;
    margin-left: -2px;
    transform-origin: 2.5% 100%;
    transform: rotate(0);
    display: none;
    z-index: 3;
}

.leaf img {
    width: 100%;
}

.center {
    width: 8.4px;
    height: 8.4px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -4.2px 0 0 -4.2px;
    z-index: 3;
}

.center img {
    width: 100%;
}

.body {
    width: 36px;
    height: 40.8px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -18px;
    z-index: 1;
}

.body img {
    width: 100%;
}

/*.body .speedbuttons {
    position: absolute;
    top: 15%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.amountbuttons {
    position: absolute;
    top: 85%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.btn {
    width: 80px;
    height: 60px;
    margin: 10px;
    font-size: 17px;
    line-height: 17px;
    border-radius: 8px;
    background-color: #eee;
    font-family: PingFang SC, Microsoft YaHei;
}
*/

@keyframes rotate {
    0% {
        transform: rotate(0);
    }

    100% {
        transform: rotate(360deg);
    }
}

#centreLeft1 {
    padding: 0.2rem;
    height: 9.125rem;
    min-width: 3.75rem;
    border-radius: 0.0625rem;

    .bg-color-black {
        height: 4.8125rem;
        border-radius: 0.125rem;
    }

    .text_chart {
        color: #c3cbde;
        font-size: 1em;
        font-weight: bold;
    }

    .body-box {
        border-radius: 0.125rem;
        overflow: hidden;
    }
}
</style>