<script setup>
    const open = ref(false)
</script>

<template>
    <div style="height: 60px;"></div>
    <nav :data-open="open">
        <div style="font-size: 18px; max-width: 1200px; margin: auto; font-weight: 600;">
            <NuxtLink to="/" style="color: unset; text-decoration: none;">
                <div class="menu-text-long">NYCU Game Design Club</div>
                <div class="menu-text-short">NYCU GDC</div>
            </NuxtLink>
        </div>
        <div class="menu-solid" @click="open = false"></div>
        <div class="menu-panel" @click="open = false">
            <NuxtLink to="/">
                <div>Home</div>
                <div style="font-size: 12px; letter-spacing: 0.2em;">首頁</div>
            </NuxtLink>
            <NuxtLink to="/news">
                <div>News</div>
                <div style="font-size: 12px; letter-spacing: 0.2em;">最新消息</div>
            </NuxtLink>
            <NuxtLink to="/events">
                <div>Event & Course</div>
                <div style="font-size: 12px; letter-spacing: 0.2em;">活動與課程</div>
            </NuxtLink>
            <NuxtLink to="/games">
                <div>Games</div>
                <div style="font-size: 12px; letter-spacing: 0.2em;">遊戲作品</div>
            </NuxtLink>
            <div class="social-links">
                <NuxtLink target="_blank" to="https://www.facebook.com/NYCUGDC">
                    <div>Facebook</div>
                </NuxtLink>
                <NuxtLink target="_blank" to="https://www.instagram.com/nycu_gdc/">
                    <div>Instagram</div>
                </NuxtLink>
                <NuxtLink target="_blank" to="https://discord.gg/7tUWM2Dj53">
                    <div>Discord</div>
                </NuxtLink>
                <NuxtLink target="_blank" to="https://nycu-gdc.itch.io/">
                    <div>Itch.io</div>
                </NuxtLink>
            </div>
        </div>
        <div class="menu-button" @click="open = !open">
            <img src="/menu_button.png" alt="" height="54" style="position: absolute;">
            <div style="height: 24px; display: flex; gap: 12px; position: relative; right: 30px;">
                <div class="menu-icon-left" style="width: 8px; height: 100%; background: var(--color2);"></div>
                <div class="menu-icon-right" style="width: 8px; height: 100%; background: var(--color2);"></div>
            </div>
        </div>
    </nav>
</template>

 <style>
    nav {
        padding: 20px;
        box-sizing: border-box;
        background-color: var(--color2);
        position: fixed;
        width: 100%;
        top: 0;
        z-index: 10;
        box-shadow: 0px 0px 5px #00000030;
    }

    .menu-button {
        position: absolute;
        height: 54px;
        top: 0;
        right: 0;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        cursor: pointer;
    }

    .menu-icon-left, .menu-icon-right {
        transition: transform 0.3s;
    }

    .menu-button:hover .menu-icon-left {
        transform: translateX(2px);
    }

    .menu-button:hover .menu-icon-right {
        transform: translateX(-2px);
    }

    .menu-text-long {
        display: block;
    }

    .menu-text-short {
        display: none;
    }

    .menu-solid {
        background-color: var(--color1);
        opacity: 0.8;
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        transition: opacity 0.3s;
    }

    nav[data-open=false] .menu-solid {
        opacity: 0;
        pointer-events: none;
    }

    .menu-panel {
        position: fixed;
        background-color: white;
        height: 100%;
        width: 240px;
        top: 0;
        right: 0;
        display: flex;
        flex-direction: column;
        gap: 20px;
        padding: 120px 32px;
        text-align: right;
        transition: transform 0.3s;
    }

    .menu-panel .router-link-active {
        color: var(--color5);
    }

    nav[data-open=false] .menu-panel {
        transform: translateX(100%);
    }

    .menu-panel > a {
        text-decoration: none;
        color: var(--color1);
        font-size: 24px;
        font-weight: 600;
    }

    .menu-panel .social-links {
        display: flex;
        flex-direction: column;
        gap: 12px;
        margin-top: 30px;
    }

    .menu-panel .social-links > a {
        text-decoration: none;
        color: var(--color1);
        font-size: 12px;
    }

    @media (max-width: 800px) {
        .menu-text-long {
            display: none;
        }

        .menu-text-short {
            display: block;
        }

        .menu-button {
            width: 100px;
        }
    }
 </style>