<template>
    <div class="banner">
        <!--ここにtransitionを追加-->
        <transition-group
            tag="div"
            appear
            @before-enter="textBeforeEnter"
            @enter="textEnter"
            class="text-container"
        >
            <div
                v-for="(line, index) in lines"
                :key="line.phrase"
                class="text"
                :data-index="index"
            >
                <div>
                    {{ line.phrase }}
                </div>
            </div>
        </transition-group>
        <div class="shape-container">
            <transition
                appear
                @before-enter="ballBeforeEnter"
                @enter="ballEnter"
            >
                <svg class="circle" width="203" height="203" viewBox="0 0 203 203" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <transition
                        appear
                        @before-enter="circleBeforeEnter"
                        @enter="circleEnter"
                    >
                        <circle cx="101.5" cy="101.5" r="101.5" fill="#14B8A6"/>
                    </transition>
                </svg>
            </transition>
        </div>
        <!--ここでtransitionをクローズ-->
    </div>
</template>

<script>
import { ref } from "vue"
import gsap from "gsap"

export default {
    setup() {
        // 表示するテキストを設定
        const lines = ref([
            { phrase: "Vue3 &" },
            { phrase: "GSAP" },
            { phrase: "PRACTICE" },
        ])
        // ここにアニメーションを追加
        const textBeforeEnter = (el) => {
            gsap.set(el, {
                y: "-100%",
                opacity: 0
            })
        }

        const textEnter = (el, done) => {
            gsap.to(el, {
                opacity: 1,
                duration: 1.2,
                y: "0",
                ease: "bounce.out",
                delay: 2 + 0.4 * (lines.value.length - el.dataset.index),
                onComplete: done
            })
        }

        const ballBeforeEnter = (el) => {
            gsap.set(el, {
                y: "-150%"
            })
        }

        const ballEnter = (el, done) => {
            const tl = gsap.timeline({delay: 5, onComplete: done})
            const screenWidth = window.innerWidth
            const elementWidth = document.querySelector(".circle").getBoundingClientRect().right
            let bouceHeight = (window.matchMedia("(max-width: 640px)").matches) ? 150 : 350
            tl.to(el, { y: bouceHeight })
            tl.to(el, { y: 0, duration: 0.5 })
            tl.to(el, { y: bouceHeight, duration: 1.25, ease: "bounce.out" })
            tl.to(el, { x: screenWidth - elementWidth - 10, duration: 2.5 }, "-=1.75")
            tl.to(el, { x: 0, duration: 1 }, "+=1")
        }

        const circleBeforeEnter = (el) => {
            gsap.set(el, {
                fill: "#F734EC"
            })
        }

        const circleEnter = (el, done) => {
            const tl = gsap.timeline({delay: 4, onComplete: done})
            tl.to(el, { fill: "#F734EC" })
            tl.to(el, { fill: "#F7C602", duration: 5.25 })
            tl.to(el, { fill: "#14B8A6", duration: 2 })
        }
        
        return { lines, textBeforeEnter, textEnter, circleEnter, ballBeforeEnter, ballEnter, circleBeforeEnter }
    }
}
</script>

<style scoped>
.banner {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 7.6rem;
}

.text {
    font-size: 5rem;
    line-height: 1;
    font-weight: 600;
}

.circle {
    position: absolute;
    width: 9rem;
    height: 9rem;
    top: -3.5rem; /** アニメーション適用後に-1.2remに編集 */
}

@media (max-width: 1024px) {
    .text {
        font-size: 3.5rem;
    }

    .circle {
        width: 4.5rem;
        height: 4.5rem;
        top: 1rem;
    }
}

@media (max-width: 640px) {
    .circle {
      top: 1.5rem;
      left: 1.5rem;
    }
}

</style>
