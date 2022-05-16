<template>
    <div class="header">
        <!--ここからtransitionコードを開始-->
        <!-- ヘッダーのアニメーション -->
        <transition
            appear
            @before-enter="headerBeforeEnter"
            @enter="headerEnter"
        >
        <div class="header-container">
            <div class="header-title">
                <span class="header-title-text">Vue3 & GSAP PRACTICE</span>
            </div>
            <transition
                appear
                @beforeEnter="linksBeforeEnter"
                @enter="linksEnter"
            >
                <div class="links-container">
                    <div class="links">
                        <a href="/">Replay</a>
                        <a href="https://github.com/kyooheeey/practice_gsap-vue3" target="_blank">GitHub</a>
                        <a href="https://twitter.com/TOKYO_KNOWHOW" target="_blank">Twitter</a>
                    </div>
                </div>
            </transition>
        </div>
        <!--ここでtransitionをクローズ-->
        </transition>
    </div>
</template>

<script>
// ここにGSAPのインポートとアニメーションのメソッドを追加
import gsap from "gsap"

export default {
    setup(){
        const headerBeforeEnter = (el) => {
            gsap.set(el, {
                y: "-100%",
                opacity: 0
            })
        }

        const headerEnter = (el, done) => {
            gsap.to(el, {
                opacity: 1,
                duration: 1,
                y: "0",
                ease: "Power0.easeOut",
                onComplete: done
            })
        }

        const linksBeforeEnter = (el) => {
            el.style.opacity= 0
        }

        const linksEnter =(el, done) => {
            gsap.to(el, {
                duration: 1,
                opacity: 1,
                delay: 1,
                onComplete: done
            })
        }

        return {headerBeforeEnter, linksBeforeEnter, headerEnter, linksEnter}
    }
}
</script>

<style scoped>
.header-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    background-color: #14B8A6;
    padding: 1.5rem;
}

.header-title {
    flex-shrink: 0;
    color: #ffffff;
    margin-right: 3rem;
}

.header-title-text {
    font-weight: 600;
    font-size: 1.5rem;
    line-height: 2rem;
    letter-spacing: -0.025em;
}

.links-container {
    width: 100%;
    display: block;
    flex-grow: 1;
}

.links a {
    display: block;
    color: #ffffff;
    margin-right: 3rem;
}

.links a:hover {
    color: #115e59;
}

@media (min-width: 1024px) {
  .links-container {
    display: flex;
    align-items: center;
    width: auto;
  }

  .links a {
    display: inline-block;
  }
}

</style>