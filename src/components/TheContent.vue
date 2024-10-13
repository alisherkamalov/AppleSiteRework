<template>
    <ul class="scroll-container" ref="scrollContainer">
        <li class="section one">
            <div class="wrapper-top">
                iPhone 16 Pro
                <span class="title">Hello, Apple Intelligence.</span>
            </div>
            <div class="bg on"></div>
            <div class="wrapper-bottom">
                <button class="learn">
                    Learn more
                </button>
                <a href="https://www.apple.com/shop/buy-iphone/iphone-16-pro">
                    <button class="buy">
                        Buy
                    </button>
                </a>

            </div>
            <span class="bottom-title">Apple Intelligence coming this fall</span>
        </li>
        <li class="section two">
            <div class="wrapper-top">
                iPhone 16
                <span class="title">Hello, Apple Intelligence.</span>
            </div>
            <div class="bg tw"></div>
            <div class="wrapper-bottom">
                <button class="learn">
                    Learn more
                </button>
                <a href="https://www.apple.com/shop/buy-iphone/iphone-16">
                    <button class="buy">
                        Buy
                    </button>
                </a>

            </div>
            <span class="bottom-title">Apple Intelligence coming this fall</span>
        </li>
        <li class="section three">
            <div class="wrapper-top watch">
                <img src="../public/watchlogo.png" alt="" class="watchlogo">
                <span class="title w">Thinstant classic.</span>
            </div>
            <div class="bg th"></div>
            <div class="wrapper-bottom watch">
                <button class="learn">
                    Learn more
                </button>
                <a href="https://www.apple.com/shop/buy-watch/apple-watch">
                    <button class="buy">
                        Buy
                    </button>
                </a>

            </div>
        </li>
        <li class="section four">
            <div class="wrapper-top ipad">
                iPad Pro
                <span class="titleipad">Thinpossible.</span>
            </div>
            <div class="bg fr"></div>
            <span class="bottom-title ipad">From $999 or $83.25/mo. for 12 mo.*</span>
            <div class="wrapper-bottom ipad">
                <a href="https://www.apple.com/shop/buy-ipad/ipad-pro">
                    <button class="buy ipad">
                        Buy
                    </button>
                </a>

            </div>
        </li>
    </ul>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const scrollContainer = ref(null);
let currentSection = ref(0);
let isScrolling = false;
const sections = ref([]);
const scrollToSection = (index) => {
    if (index < 0 || index >= sections.value.length) return;
    currentSection.value = index;

    sections.value.forEach((section, i) => {
        section.style.height = (i === currentSection.value) ? '100dvh' : '0dvh';


        const wrapperTop = section.querySelector('.wrapper-top');
        if (wrapperTop) {
            wrapperTop.style.opacity = (i === currentSection.value) ? '1' : '0';
            wrapperTop.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
        }
        const wrapperBottom = section.querySelector('.wrapper-bottom');
        if (wrapperBottom) {
            wrapperBottom.style.opacity = (i === currentSection.value) ? '1' : '0';
            wrapperBottom.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
        }
        const bottomTitle = section.querySelector('.bottom-title');
        if (bottomTitle) {
            bottomTitle.style.opacity = (i === currentSection.value) ? '1' : '0';
            bottomTitle.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
        }
        if (currentSection.value === 4) {
            const wrapperTop = section.querySelector('.wrapper-top');
            if (wrapperTop) {
                wrapperTop.style.opacity = (i === currentSection.value) ? '1' : '0';
                wrapperTop.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
                wrapperTop.style.scale = (i === currentSection.value) ? '0.8' : '1';
            }
            const wrapperBottom = section.querySelector('.wrapper-bottom');
            if (wrapperBottom) {
                wrapperBottom.style.opacity = (i === currentSection.value) ? '1' : '0';
                wrapperBottom.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
                wrapperBottom.style.scale = (i === currentSection.value) ? '0.8' : '1';
            }
            const bottomTitle = section.querySelector('.bottom-title');
            if (bottomTitle) {
                bottomTitle.style.opacity = (i === currentSection.value) ? '1' : '0';
                bottomTitle.style.translate = (i === currentSection.value) ? '0px -50px' : '0px 0px';
                bottomTitle.style.scale = (i === currentSection.value) ? '0.8' : '1';
            }
        }
    });
};

const handleWheel = (event) => {
    if (isScrolling) return;
    event.preventDefault();
    isScrolling = true;

    if (event.deltaY > 0) {
        scrollToSection(currentSection.value + 1);
    } else {
        scrollToSection(currentSection.value - 1);
    }
    if (currentSection.value === 3) {
        document.body.style.overflow = 'visible';
        const footer = document.querySelector('.container');
        if (footer) {
            footer.style.display = 'flex';
        }
    }
    setTimeout(() => {
        isScrolling = false;
    }, 500);
};

let startY = 0;

const handleTouchStart = (event) => {
    startY = event.touches[0].clientY;
};

const handleTouchEnd = (event) => {
    const endY = event.changedTouches[0].clientY;
    if (Math.abs(startY - endY)) {
        scrollToSection(currentSection.value + (startY > endY ? 1 : -1));
    }
    if (window.innerWidth <= 1000) {
        if (currentSection.value === 3) {
            document.body.style.overflow = 'visible';
            const footer = document.querySelector('.container');
            if (footer) {
                footer.style.display = 'flex';
            }
            window.scrollTo(1, 0);
        }
    }

};
let intervalId;
let swipeTimeout;

const startAutoScroll = () => {
    intervalId = setInterval(() => {
        currentSection.value += 1;

        if (currentSection.value === 3) {
            document.body.style.overflow = 'visible';
            const footer = document.querySelector('.container');
            if (footer) {
                footer.style.display = 'flex';
                window.scrollTo(1, 0);
            }
        }
        if (currentSection.value === 4) {
            currentSection.value = 0;
        }

        scrollToSection(currentSection.value);
    }, 2000);
};

const handleUserInteraction = () => {
    clearInterval(intervalId);
    clearTimeout(swipeTimeout);


    swipeTimeout = setTimeout(() => {
        startAutoScroll();
    }, 3000);
};

const initializeScroll = () => {
    sections.value = Array.from(scrollContainer.value.children);
    scrollContainer.value.addEventListener('wheel', handleWheel);
    scrollContainer.value.addEventListener('touchstart', handleTouchStart);
    scrollContainer.value.addEventListener('touchend', handleTouchEnd);
    document.body.style.overflow = 'hidden';
    window.scrollTo(0, 0);
    scrollToSection(0);

    startAutoScroll();


    scrollContainer.value.addEventListener('touchstart', handleUserInteraction);
    scrollContainer.value.addEventListener('wheel', handleUserInteraction);
};

onMounted(() => {
    initializeScroll();
});

onBeforeUnmount(() => {
    clearInterval(intervalId);
    clearTimeout(swipeTimeout);
    scrollContainer.value.removeEventListener('wheel', handleWheel);
    scrollContainer.value.removeEventListener('touchstart', handleTouchStart);
    scrollContainer.value.removeEventListener('touchend', handleTouchEnd);
});

</script>
<style scoped>
.scroll-container {
    height: 100vh;
    overflow: hidden;
}

.watchlogo {
    height: 80px;
}

.learn {
    font-size: 17px;
    line-height: 1.17648;
    font-weight: 400;
    letter-spacing: -.022em;
    font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    border-style: solid;
    border-width: 1px;
    min-width: 28px;
    padding-left: 21px;
    padding-right: 21px;
    padding-top: 11px;
    padding-bottom: 11px;
    --sk-button-margin-horizontal: 18px;
    --sk-button-margin-vertical: 18px;
    color: #fff;
    background: #0071e3;
    border-color: rgba(0, 0, 0, 0);
    border-radius: 980px;
    pointer-events: all;
}

.learn:active {
    background-color: #0077ed;
}

.learn:hover {
    background-color: #0077ed;
}

.titleipad {
    display: inline-block;
    background-clip: text;
    -webkit-text-fill-color: rgba(0, 0, 0, 0);
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;
    background-repeat: no-repeat;
    background-image: url(../public/bgtitle.jpg);
    background-position: bottom;
    background-size: 100% 90%;
    margin-top: 7px;
    z-index: 3;
    font-size: 64px;
    line-height: 1.0625;
    font-weight: 600;
    letter-spacing: -0.009em;
    font-family: SF Pro Display, SF Pro Icons, Helvetica Neue, Helvetica, Arial, sans-serif;
}

.buy {
    margin-left: 13px;
    pointer-events: all;
    background: rgba(0, 0, 0, 0);
    color: #2997ff;
    border-color: #2997ff;
    font-size: 17px;
    line-height: 1.17648;
    font-weight: 400;
    letter-spacing: -.022em;
    font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    border-style: solid;
    border-width: 1px;
    min-width: 28px;
    padding-left: 21px;
    padding-right: 21px;
    padding-top: 11px;
    padding-bottom: 11px;
    --sk-button-margin-horizontal: 18px;
    --sk-button-margin-vertical: 18px;
    border-radius: 980px;
}

.w {
    color: black;
    font-weight: 400;
}

.buy:active {
    background-color: #0071e3;
    border-color: #0071e3;
    color: #fff;
}

.buy:hover {
    background-color: #0071e3;
    border-color: #0071e3;
    color: #fff;
}

.section {
    height: 0vh;
    transition: height 0.5s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    color: white;
    overflow: hidden;
    align-items: flex-start;
    background-color: transparent;
    position: relative;
}

.bg {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
}

.title {
    font-size: 24px;
    line-height: 1.16667;
    font-weight: 400;
    letter-spacing: .009em;
    font-family: "SF Pro Display", "SF Pro Icons", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    margin-top: 5px;
}

.wrapper-top {
    width: 100%;
    display: flex;
    font-size: 52px;
    line-height: 1.08349;
    font-weight: 600;
    transition: all 0.5s ease;
    letter-spacing: -.002em;
    font-family: "SF Pro Display", "SF Pro Icons", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
    flex-direction: column;
    align-items: center;
    margin-top: 121px;
    color: #f5f5f7;
}

.wrapper-bottom {
    width: 100%;
    position: absolute;
    bottom: 101px;
    display: flex;
    transition: all 0.5s ease;
    justify-content: center;
    pointer-events: all;
}

.watch {
    top: 251px;
    bottom: auto;
    z-index: 1;
}

.watcht {
    top: 61px;
    bottom: auto;
}

.bottom-title {
    width: 100%;
    position: absolute;
    bottom: 61px;
    transition: all 0.5s ease;
    display: flex;
    color: #86868b;
    justify-content: center;
    font-size: 19px;
    line-height: 1.21053;
    font-weight: 400;
    letter-spacing: .012em;
    font-family: "SF Pro Display", "SF Pro Icons", "Helvetica Neue", "Helvetica", "Arial", sans-serif;
}

.bottom-title.ipad {
    color: #fff;
}

.ipad {
    bottom: 31px;
    transition: all 1.5s ease;
}

.wrapper-bottom.ipad {
    bottom: 71px;
}

.buy.ipad {
    margin-left: 0;
    transition: none;
}

.bg.on {
    background-image: url(../public/i16prosmall.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;

}

.bg.tw {
    background-image: url(../public/i16small.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
}

.bg.th {
    background-image: url(../public/watchbig.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
}

.bg.fr {
    background-image: url(../public/ipadbig.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
}

@media (min-width:2500px) {
    .bg.on {
        background-image: url(../public/i16probig.jpg);
    }

    .bg.tw {
        background-image: url(../public/i16big.jpg);
    }

    .bg.th {
        background-image: url(../public/watchbig.jpg);
    }

    .bg.fr {
        background-image: url(../public/ipadbig.jpg);
    }
}

@media (max-width:1300px) {
    .bg.on {
        background-image: url(../public/i16prosmall.jpg);
    }

    .bg.tw {
        background-image: url(../public/i16small.jpg);
    }

    .bg.th {
        background-image: url(../public/watchsmall.jpg);
    }

    .bg.fr {
        background-image: url(../public/ipadbig.jpg);
    }
}

@media (max-width:900px) {
    .bg.on {
        background-image: url(../public/i16prossmall.jpg);
    }

    .bg.tw {
        background-image: url(../public/i16ssmall.jpg);
    }

    .bg.th {
        background-image: url(../public/watchssmall.jpg);
    }

    .bg.fr {
        background-image: url(../public/ipadsmall.jpg);
    }

    .four {
        background-color: #000000;
        justify-content: center;
    }

    .bg.fr {
        z-index: 0;
        width: 540px;
        scale: 0.7;
        top: 20px;
        left: auto;

    }

    .wrapper-top.watch {
        margin-top: 100px;
    }

    .wrapper-bottom.watch {
        top: 230px;
    }

    .wrapper-top.ipad {
        z-index: 1;
        margin-top: 70px;
        font-size: 32px;
    }

    .titleipad {
        font-size: 34px;
    }
}
</style>
