<template>
    <div>
        <div class="windmill">
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
            <div class="leaf"><img src="../../../assets/leaf.png"></div>
        </div>
        <div class="bg">
            <div class="center"><img src="../../../assets/center.png"></div>
            <div class="body"><img src="../../../assets/body.png"></div>
        </div>
        <div class="speedbuttons">
            <button class="btn speedup">Speed Up</button>
            <button class="btn speeddown">Speed Down</button>
        </div>
        <div class="amountbuttons">
            <button class="btn amountup">Amount Up</button>
            <button class="btn amountdown">Amount Down</button>
        </div>
    </div>
</template>

<script>
export default {
    mounted() {
        let su = document.querySelector(".speedup"),
            sd = document.querySelector(".speeddown"),
            au = document.querySelector(".amountup"),
            ad = document.querySelector(".amountdown"),
            wm = document.querySelector(".windmill"),
            s = 3,
            a = 3,
            lf = document.getElementsByClassName('leaf');

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

        sd.onclick = () => {
            s += 0.2;
            setup();
        };

        su.onclick = () => {
            if (s > 0.1) {
                s -= 0.1;
                setup();
            }
        };

        ad.onclick = () => {
            if (a > 3) {
                a -= 1;
                setup();
            }
        };

        au.onclick = () => {
            if (a < 8) {
                a += 1;
                setup();
            }
        };

        setup();
    },
};
</script>

<style>
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
    width: 310.4px;
    height: 310.4px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -155.2px 0 0 -155.2px;
    /*border: solid 1px red;*/
    /*background-color: white;*/
    animation-name: rotate;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
}

.leaf {
    width: 50.4px;
    height: 155.2px;
    /*border: 125px 25px 0 25px;*/
    position: absolute;
    top: 0;
    left: 50%;
    margin-left: -4px;
    /*background-color: #fff;*/
    transform-origin: 2.5% 100%;
    transform: rotate(0);
    display: none;
}

.leaf img {
    width: 100%;
}

.center {
    width: 33.6px;
    height: 33.6px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -16.8px 0 0 -16.8px;
}

.center img {
    width: 100%;
}

.body {
    width: 144px;
    height: 163.2px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -72px;
    z-index: -1;
}

.body img {
    width: 100%;
}

.speedbuttons {
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

@keyframes rotate {
    0% {
        transform: rotate(0);
    }

    100% {
        transform: rotate(360deg);
    }
}
</style>