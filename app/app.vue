<script setup>
    import gsap from 'gsap'
    
    import { ScrollTrigger } from 'gsap/ScrollTrigger'

    gsap.registerPlugin(ScrollTrigger)

    useHead({
        link: [
            { rel: 'icon', type: 'image', href: '/icon.png' }
        ]
    })

    function scrollToTop() {
        scroll({ top: 0, behavior: 'smooth' })
    }
    
    useSeoMeta({
        lang: 'zh-tw',
        themeColor: '#ff9100',
        titleTemplate: titleChunk => (titleChunk? `${titleChunk} | NYCU GDC 遊戲設計社` : `NYCU GDC 遊戲設計社`),
        ogTitle: 'NYCU GDC 遊戲設計社',
        description: '陽明交大遊戲設計社（NYCU GDC），誠徵邀請對遊戲製作、虛擬實境、動畫/角色/場景建模有興趣的你 (不論科系)，在大學期間與夥伴一起玩遊戲、做遊戲！',
        ogDescription: '陽明交大遊戲設計社（NYCU GDC），誠徵邀請對遊戲製作、虛擬實境、動畫/角色/場景建模有興趣的你 (不論科系)，在大學期間與夥伴一起玩遊戲、做遊戲！',
        ogSiteName: 'NYCU GDC 遊戲設計社',
        ogUrl: 'https://www.nycu-gdc.org/',
        ogImage: 'https://www.nycu-gdc.org/site_image.png'
    })
</script>

<template>
    <NuxtLoadingIndicator color="#ff9100" />
    <MenuBar />
    <NuxtPage />
    <footer>
        <div style="width: 100%; position: relative; overflow: hidden; background-color: var(--color3);">
            <div style="font-weight: 900; font-size: 80px; color: var(--color2); position: absolute; white-space: nowrap; opacity: 0.1; top: 100px; animation: scroll 25s infinite linear;">
                <span style="display: inline-block; padding-right: 30px">Fun to Play, Play to Live, Live for Fun</span>
                <span style="display: inline-block; padding-right: 30px">Fun to Play, Play to Live, Live for Fun</span>
            </div>
            <div style="max-width: 1200px; width: 90%; margin: auto; text-align: center; padding: 100px 0; position: relative;">
                <div style="font-size: 24px; color: white; margin-bottom: 20px; letter-spacing: 0.05em;">加入我們，一起做遊戲！</div>
                <NuxtLink class="button" target="_blank" to="https://discord.gg/7tUWM2Dj53">
                    <div>Discord 社群</div>
                </NuxtLink>
                <NuxtLink class="button" target="_blank" to="https://linktr.ee/nycugdc" style="background-color: var(--color1); color: white;">
                    <div>其他連結</div>
                </NuxtLink>
            </div>
        </div>
        <div style="background-color: var(--color1);">
            <div style="max-width: 1200px; width: 90%; margin: auto; color: white; padding: 60px 0;">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                    <div>
                        <div style="display: flex; gap: 8px; align-items: center;">
                            <div style="background-image: url('/logo_white.png'); background-size: 120%; background-position: center; width: 80px; height: 50px;"></div>
                            <div style="font-size: 16px; letter-spacing: 0.2em;"><span style="font-size: 10px;">陽明交通大學</span><br>遊戲設計社</div>
                        </div>
                    </div>
                    <div style="font-size: 24px; font-weight: 600; color: var(--color3); cursor: pointer;" @click="scrollToTop">TOP</div>
                </div>
                <div style="display: flex; gap: 16px; margin-left: 6px;">
                    <NuxtLink to="/">
                        <div>Home</div>
                    </NuxtLink>
                    <NuxtLink to="/news">
                        <div>News</div>
                    </NuxtLink>
                    <NuxtLink to="/events">
                        <div>Event & Course</div>
                    </NuxtLink>
                    <NuxtLink to="/games">
                        <div>Games</div>
                    </NuxtLink>
                </div>
            </div>
        </div>
    </footer>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@100..900&family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');
    
    :root {
        --color1: #546375;
        --color2: #e4e9f2;
        --color3: #93aac1;
        --color4: #2cc2ff;
        --color5: #ff9100;
    }

    body {
        margin: 0;
        font-family: 'Rubik', 'Noto Sans TC';
        color: var(--color1);
    }

    .button {
        background-color: var(--color2);
        padding: 12px;
        margin: 4px;
        width: 120px;
        text-decoration: none;
        color: var(--color1);
        display: inline-block;
        letter-spacing: 0.05em;
        font-size: 15px;
        font-weight: 600;
        border-radius: 32px;
        transition-duration: 0.2s;
    }

    .button:hover {
        background-color: var(--color5) !important;
        color: white !important;
    }

    footer a {
        color: var(--color3);
        font-size: 12px;
        letter-spacing: 0.1em;
    }

    .news {
        display: grid;
        gap: 12px;
        grid-template-columns: 1fr;
    }
    
    .news article {
        transition-duration: 0.2s;
        border: solid 1px var(--color2);
        padding: 12px;
    }

    .news article:hover {
        color: var(--color5);
        border-color: var(--color5);
    }

    @keyframes scroll {
        from { transform: translateX(0); }
        to { transform: translateX(-50%); }
    }

    .page-enter-active, .page-leave-active {
        transition: all 0.3s;
    }

    .page-enter-from, .page-leave-to {
        opacity: 0;
    }
</style>