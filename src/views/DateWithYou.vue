<template>
	<a-row>
		<a-col :span="24">
            <Navi v-on:change-bg="changeBg"></Navi>
		</a-col>
		<a-col :xs="{ span:24 }" :sm="{ span: 24 }" :md="{ span:16, offset:4 }" :lg="{ span:12, offset:6 }" :xl="{ span: 12, offset: 6 }" :xxl="{ span: 12, offset: 6 }">
            <router-view />
        </a-col>
        <canvas id="evanyou-canvas" class="evan-you"></canvas>
    </a-row>
</template>
<script>
	import Navi from '../components/Navi.vue';
	export default {
		name: 'DateWithYou',
		components: {
			Navi,
        },
        methods: {
            initBg() {
                document.addEventListener('touchmove', function(e) {
                    e.preventDefault();
                });
                let c = document.querySelector('#evanyou-canvas');
                let x = c.getContext('2d');
                let pr = window.devicePixelRatio || 1;
                let w = window.innerWidth;
                let h = window.innerHeight;
                let f = 90;
                let q;
                let m = Math;
                let r = 0;
                let u = m.PI * 2;
                let v = m.cos;
                let z = m.random;
                c.width = w * pr;
                c.height = h * pr;
                x.scale(pr, pr);
                x.globalAlpha = 0.6;
                function init() {
                    x.clearRect(0, 0, w, h);
                    q = [{ x: 0, y: h * 0.7 + f }, { x: 0, y: h * 0.7 - f }];
                    while (q[1].x < w + f) d(q[0], q[1]);
                }
                function d(i, j) {
                    x.beginPath();
                    x.moveTo(i.x, i.y);
                    x.lineTo(j.x, j.y);
                    let k = j.x + (z() * 2 - 0.25) * f;
                    let n = y(j.y);
                    x.lineTo(k, n);
                    x.closePath();
                    r -= u / -50;
                    x.fillStyle =
                        '#' +
                        (
                            ((v(r) * 127 + 128) << 16) |
                            ((v(r + u / 3) * 127 + 128) << 8) |
                            (v(r + (u / 3) * 2) * 127 + 128)
                        ).toString(16);
                    x.fill();
                    q[0] = q[1];
                    q[1] = { x: k, y: n };
                }
                function y(p) {
                    let t = p + (z() * 2 - 1.1) * f;
                    return t > h || t < 0 ? y(p) : t;
                }
                // document.onclick = init;
                document.ontouchstart = init;
                init();
            },
            changeBg() {
                this.initBg();
            },
        },
		mounted() {
			this.initBg();
		},
	};
</script>
<style scoped>
    .evan-you {
		position: fixed;
		top: 47.4px;
		left: 0px;
		z-index: -10;
		width: 100%;
		pointer-events: none;
	}
</style>
