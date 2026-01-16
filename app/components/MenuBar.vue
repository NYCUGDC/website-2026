<script setup>
    const open = ref(false)
</script>

<template>
    <nav :data-open="open">
        <div style="font-size: 18px; max-width: 1200px; margin: auto; font-weight: 600;">
            <NuxtLink to="/" style="color: var(--color1); text-decoration: none;">
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
                <div style="margin-bottom: 16px; color: var(--color3);">社群連結</div>
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
            <div style="position: absolute; height: 120px; width: 120px; background-image: url('/gdc-character.png'); background-size: cover; bottom: 0; right: 90px; filter: invert(1); opacity: 0.1;"></div>
        </div>
        <div class="menu-button" @click="open = !open">
            <img src="/menu_button.png" alt="" height="40" style="position: absolute;">
            <div style="height: 20px; display: flex; gap: 12px; position: relative; right: 30px;">
                <div class="menu-icon-left" style="width: 8px; height: 100%; background: white;"></div>
                <div class="menu-icon-right" style="width: 8px; height: 100%; background: white;"></div>
            </div>
        </div>
    </nav>
</template>

 <style>
    nav {
        padding: 12px 24px;
        box-sizing: border-box;
        position: fixed;
        width: 100%;
        top: 0;
        z-index: 10;
    }

    .menu-button {
        position: absolute;
        height: 40px;
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
        width: 300px;
        top: 0;
        right: 0;
        display: flex;
        flex-direction: column;
        gap: 20px;
        padding: 100px 32px;
        text-align: right;
        transition: transform 0.3s;
        box-sizing: border-box;
    }

    .menu-panel .router-link-active {
        color: var(--color1);
    }

    nav[data-open=false] .menu-panel {
        transform: translateX(100%);
    }

    .menu-panel > a {
        text-decoration: none;
        color: var(--color3);
        font-size: 24px;
        font-weight: 600;
        transition-duration: 0.2s;
    }

    .menu-panel > a:hover, .menu-panel .social-links > a:hover {
        color: var(--color5);
    }

    .menu-panel .social-links {
        display: flex;
        flex-direction: column;
        gap: 12px;
        margin-top: 30px;
    }

    .menu-panel .social-links > a {
        text-decoration: none;
        color: var(--color3);
        font-size: 12px;
        transition-duration: 0.2s;
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