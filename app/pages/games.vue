<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "games", queries: { limit: 50 } }, { key: 'games' })
    const openGame = ref(null)

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleDateString('zh-TW')
    }

    useSeoMeta({
        title: '遊戲作品'
    })
</script>

<template>
    <section style="margin: 200px 0px;">
        <div style="max-width: 1200px; width: 90%; margin: auto;">
            <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">遊戲作品</div>
            <h1 style="color: var(--color5); margin-top: 8px;">Games</h1>
            <p style="color: var(--color3);">本頁面收錄了在遊戲接龍與 GameJam 等活動中，由社員們一起創作的遊戲作品！</p>
            <div class="game" v-if="data?.contents?.length">
                <article v-for="game in data?.contents" @click="openGame = game">
                    <div style="overflow: hidden;">
                        <img class="game-img" :src="game?.image?.url" alt="" draggable="false">
                    </div>
                    <div style="padding: 8px;">
                        <h2 style="margin: 0 0 4px 0; font-size: 16px;">{{ game?.name }}</h2>
                        <ClientOnly>
                            <div style="font-size: 12px; color: var(--color3);">{{ convertDate(game?.date) }}</div>
                        </ClientOnly>
                    </div>
                </article>
            </div>
        </div>
        <div v-if="openGame" style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: var(--color1); opacity: 0.8; z-index: 20;"></div>
        <Transition name="pop">
            <div class="open-game" v-if="openGame">
                <div class="open-game-window">
                    <div style="overflow: scroll; height: 100%;">
                        <div class="open-game-content">
                            <div style="width: 100%; max-width: 360px; position: relative; text-align: center;">
                                <img :src="openGame?.image?.url" alt="" draggable="false" style="width: 100%;">
                                <h2>{{ openGame?.name }}</h2>
                                <div>
                                    <div style="font-size: 15px; color: var(--color3);">{{ convertDate(openGame?.date) }}</div>
                                    <div v-if="openGame?.event" style="font-size: 15px; color: var(--color3);">{{ openGame?.event }}</div>
                                </div>
                                <NuxtLink v-if="openGame?.link" target="_blank" :to="openGame?.link" style="text-decoration: none;">
                                    <div class="button" style="background-color: var(--color1); color: white; text-align: center; margin-top: 20px;">
                                        開啟連結
                                    </div>
                                </NuxtLink>
                            </div>
                            <div class="open-game-description">{{ openGame.description }}</div>
                        </div>
                    </div>
                    <div class="close-button" style="cursor: pointer; position: absolute; top: 16px; right: 16px; display: flex; justify-content: center; align-items: center; width: 32px; height: 32px; background-color: white; border-radius: 18px;" @click="openGame = null">
                        <div style="position: absolute; width: 2px; height: 16px; background-color: var(--color3); transform: rotate(45deg);"></div>
                        <div style="position: absolute; width: 2px; height: 16px; background-color: var(--color3); transform: rotate(-45deg);"></div>
                    </div>
                </div>
            </div>
        </Transition>
    </section>
</template>

<style>
    .game {
        text-align: center;
        margin-top: 100px;
        display: grid;
        gap: 12px;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }

    .game article {
        border: solid 1px var(--color2);
        overflow: hidden;
        position: relative;
        cursor: pointer;
        transition-duration: 0.2s;
        background-color: white;
        border-radius: 8px;
    }

    .game article:hover {
        color: var(--color5);
        border-color: var(--color5);
    }

    .game-img {
        width: 100%;
        aspect-ratio: 1.4;
        object-fit: cover;
        transition: transform 0.6s;
        display: block;
    }

    article:hover .game-img {
        transform: scale(1.1);
    }

    .open-game {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        z-index: 20;
    }

    .open-game-window {
        position: absolute;
        top: 40px;
        right: 40px;
        bottom: 40px;
        left: 40px;
        background-color: var(--color2);
        border-radius: 20px;
    }

    .open-game-content {
        display: flex;
        flex-wrap: wrap;
        padding: 80px 60px 60px 60px;
        gap: 60px;
        line-height: 1.8;
    }

    .open-game-description {
        white-space: pre-wrap;
    }

    .pop-enter-active, .pop-leave-active {
        transition: all 0.3s;
    }

    .pop-enter-from, .pop-leave-to {
        transform: scale(0);
    }

    @media (max-width: 800px) {
        .open-game-window {
            top: 20px;
            right: 20px;
            bottom: 20px;
            left: 20px;
        }
        
        .open-game-content {
            padding: 60px 16px;
        }

        .open-game-description {
            font-size: 13px;
        }
    }
</style>