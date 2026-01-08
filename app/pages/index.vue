<script setup>
    import gsap from 'gsap'

    import { Draggable } from 'gsap/all'
    
    const { data } = await useMicroCMSGetList({ endpoint: "committee" }, { key: 'committee' })

    onMounted(() => {
        gsap.to('#image1', { scale: 1, delay: 0.2 })
        gsap.to('#image4', { scale: 1, delay: 0.5 })
        gsap.to('#image2', { scale: 1, delay: 0.85 })
        gsap.to('#image3', { scale: 1, delay: 0.75 })
        gsap.to('#image5', { scale: 1, delay: 0.9 })
        gsap.to('.window', { scale: 1, delay: 1 })
        Draggable.create('.window', { zIndexBoost: false })
    })
</script>

<template>
    <div>
        <header>
            <img id="image1" class="images" draggable="false" src="/tablet.png" alt="" width="172" style="transform: scale(0); position: absolute; top: 10%; left: 10%;">
            <img id="image2" class="images" draggable="false" src="/cd.png" alt="" width="75" style="transform: scale(0); position: absolute; top: 20%; left: 20%;">
            <img id="image3" class="images" draggable="false" src="/cube.png" alt="" width="77" style="transform: scale(0); position: absolute; bottom: 20%; left: 10%;">
            <img id="image4" class="images" draggable="false" src="/midi.png" alt="" width="163" style="transform: scale(0); position: absolute; bottom: 30%; right: 10%;">
            <img id="image5" class="images" draggable="false" src="/controller.png" alt="" width="56" style="transform: scale(0); position: absolute; top: 30%; right: 20%;">
            <img style="position: relative;" src="/logo.png" alt="" width="60" draggable="false">
            <h1 style="position: relative;"><span>陽明交通大學</span><br>遊戲設計社</h1>
            <div class="window">
                <p>陽明交大遊戲設計社（NYCU GDC），誠徵邀請對遊戲製作、虛擬實境、動畫／角色／場景建模有興趣的你（不論科系），在大學期間與夥伴一起玩遊戲、做遊戲！</p>
                <img src="/window_icon.png" alt="" width="60" style="position: absolute; top: 16px; right: 16px;">
            </div>
        </header>
        <section style="margin: 100px 0px;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <h2 style="font-size: 15px; color: var(--color5); letter-spacing: 0.2em;">關於本社團</h2>
                <div class="split-content" style="margin-bottom: 120px;">
                    <p style="color: var(--color2); font-weight: 900; font-size: 24px;">Fun to Play, Play to Live, Live for Fun</p>
                    <div style="display: flex; gap: 28px; letter-spacing: 0.05em;">
                        <NuxtLink to="/news" style="color: var(--color3);">最新消息</NuxtLink>
                        <NuxtLink to="/events" style="color: var(--color3);">活動與課程</NuxtLink>
                        <NuxtLink to="/games" style="color: var(--color3);">遊戲作品</NuxtLink>
                    </div>
                </div>
                <div class="about-pictures">
                    <div>
                        <img src="/event.jpeg" alt="" draggable="false">
                        <div style="font-weight: 700;">遊戲製作社課</div>
                        <p>每學期開設遊戲製作相關技術的課程提供社員參加，包括 Unity 遊戲引擎操作、程式設計與 3D 建模等。</p>
                    </div>
                    <div>
                        <img src="/event2.jpg" alt="" draggable="false">
                        <div style="font-weight: 700;">GameJam 與遊戲接龍</div>
                        <p>定期舉辦免費參與的 GameJam 與遊戲接龍等活動，讓大家能體驗短期內與他人一起合力創作遊戲的過程。</p>
                    </div>
                    <div>
                        <img src="/event3.jpg" alt="" draggable="false">
                        <div style="font-weight: 700;">講座與社群</div>
                        <p>邀請遊戲開發者舉辦實體講座分享經驗，歡迎對遊戲產業有興趣的同學一起來交流！</p>
                    </div>
                </div>
            </div>
        </section>
        <section style="padding: 120px 0px; background: var(--color2);">
            <div class="committee-list">
                <h2 style="font-size: 15px; color: var(--color1); letter-spacing: 0.2em;">社團幹部</h2>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(170px, 1fr)); gap: 10px;" v-if="data?.contents?.length">
                    <div class="committee" v-for="committee in data?.contents">
                        <img :src="committee?.avatar?.url ?? '/icon.png'" alt="" draggable="false">
                        <div style="display: flex; flex-direction: column; align-items: flex-start; justify-content: center; margin-left: 12px;">
                            <div style="font-size: 16px; font-weight: 700;">{{ committee?.name }}</div>
                            <div style="font-size: 12px; letter-spacing: 0.1em;">{{ committee?.role }}</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<style>
    header {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        height: calc(100vh - 45px);
        background: radial-gradient(var(--color2) 1px, transparent 2px);
        background-size: 50px 50px;
        border-bottom: 1px solid var(--color2);
        overflow: hidden;
    }

    header > h1 {
        text-align: center;
        font-size: 48px;
        font-weight: 300;
        letter-spacing: 0.2em;
        color: var(--color5);
        margin: 0;
        margin-top: 12px;
        line-height: 1.2;
    }

    header > h1 > span {
        font-size: 15px;
        font-weight: 600;
        letter-spacing: 0.8em;
    }

    .window {
        position: relative;
        max-width: 400px;
        color: var(--color3);
        border: 1px solid var(--color2);
        background-color: white;
        letter-spacing: 0.05em;
        padding: 30px 20px 10px 20px;
        border-radius: 8px;
        margin: 60px 16px;
        line-height: 1.8;
        font-size: 13px;
        box-shadow: 4px 4px var(--color2);
        transform: scale(0);
    }

    .about-pictures {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 40px;
    }

    .about-pictures img {
        width: 100%;
        aspect-ratio: 1.66;
        object-fit: cover;
        border-radius: 8px;
        margin-bottom: 12px;
    }

    .about-pictures p {
        font-size: 13px;
        letter-spacing: 0.1em;
        color: var(--color3);
    }
    
    .committee-list {
        max-width: 1200px;
        width: 90%;
        margin: auto;
        display: grid;
        grid-template-columns: 240px 1fr;
    }

    .committee {
        width: 100%;
        border-radius: 8px;
        overflow: hidden;
        color: var(--color3);
        background-color: white;
        display: flex;
    }

    .committee > img {
        width: 56px;
        height: 56px;
        object-fit: cover;
    }

    .split-content {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    @media (max-width: 800px) {
        .about-pictures {
            grid-template-columns: 1fr;
        }

        .split-content {
            display: block;
        }

        .images {
            opacity: 0.2;
        }
    
        .committee-list {
            display: block;
        }
    }
</style>