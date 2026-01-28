<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "committee", queries: { limit: 50 } }, { key: 'committee' })
    const news = (await useMicroCMSGetList({ endpoint: "news", queries: { limit: 3 } }, { key: 'news-home' })).data
    const events = (await useMicroCMSGetList({ endpoint: "events" }, { key: 'events-home' })).data

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleString('zh-TW')
    }
</script>

<template>
    <div>
        <header>
            <div id="bg"></div>
            <img style="position: relative;" src="/logo.png" alt="" width="60" draggable="false">
            <h1 style="position: relative;"><span>陽明交通大學</span><br>遊戲設計社</h1>
            <div class="window">
                <div style="padding: 30px 20px 10px 20px;">
                    <p>陽明交大遊戲設計社（NYCU GDC），誠徵邀請對遊戲製作、虛擬實境、動畫／角色／場景建模有興趣的你（不論科系），在大學期間與夥伴一起玩遊戲、做遊戲！</p>
                    <img src="/window_icon.png" alt="" width="60" style="position: absolute; top: 16px; right: 16px;">
                </div>
            </div>
        </header>
        <section style="margin-bottom: 100px;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <div class="about-pictures">
                    <div id="about-1">
                        <img src="/event1.jpg" alt="" draggable="false">
                        <div style="font-weight: 700;">遊戲製作社課</div>
                        <p>每學期開設遊戲製作相關技術的課程提供社員參加，包括 Unity 遊戲引擎操作、程式設計與 3D 建模等。</p>
                    </div>
                    <div id="about-2">
                        <img src="/event2.jpg" alt="" draggable="false">
                        <div style="font-weight: 700;">GameJam 與遊戲接龍</div>
                        <p>定期舉辦免費參與的 GameJam 與遊戲接龍等活動，讓大家能體驗短期內與他人一起合力創作遊戲的過程。</p>
                    </div>
                    <div id="about-3">
                        <img src="/event3.jpg" alt="" draggable="false">
                        <div style="font-weight: 700;">講座與社群</div>
                        <p>邀請遊戲開發者舉辦實體講座分享經驗，歡迎對遊戲產業有興趣的同學一起來交流！</p>
                    </div>
                </div>
            </div>
        </section>
        <section style="margin: 160px 0px;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <div class="news-events">
                    <div>
                        <h2 style="text-align: center; color: var(--color5); font-size: 28px;">News</h2>
                        <div class="news" v-if="news?.contents?.length">
                            <NuxtLink v-for="news in news?.contents" :to="'/news/' + news?.slug" style="text-decoration: unset; color: unset; position: relative;">
                                <article>
                                    <h2 style="margin: 0 0 12px 0; font-size: 18px; font-weight: 600;">{{ news?.title }}</h2>
                                    <ClientOnly>
                                        <div style="font-size: 12px; color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">發布時間</span>{{ convertDate(news?.publishedAt) }}</div>
                                    </ClientOnly>
                                    <div style="position: absolute; height: 100%; width: 120px; background-image: url('/gdc-character.png'); background-size: cover; top: 0; right: 20px; filter: invert(1); opacity: 0.1;"></div>
                                </article>
                            </NuxtLink>
                        </div>
                        <div style="text-align: center; margin-top: 20px;">
                            <NuxtLink class="button" to="/news" style="background-color: var(--color1); color: white;">
                                <div>更多最新消息</div>
                            </NuxtLink>
                        </div>
                    </div>
                    <div>
                        <h2 style="text-align: center; color: var(--color5); font-size: 28px;">Event & Course</h2>
                        <div v-if="events?.contents?.length" style="display: grid; gap: 12px;">
                            <div v-if="!events?.contents?.filter(e => !e?.ended)?.length" style="display: flex; align-items: center; justify-content: center; color: var(--color3); background-color: var(--color2); padding: 20px; border-radius: 8px;">
                                活動準備中，敬請期待！
                            </div>
                            <div v-for="event in events?.contents?.filter(e => !e?.ended)" style="position: relative; height: 100px; border: solid 1px var(--color2); display: flex; align-items: center;">
                                <img :src="event?.image?.url ?? '/logo.png'" alt="" draggable="false" style="height: 100%; aspect-ratio: 1.5; object-fit: cover;">
                                <div style="padding: 16px; color: var(--color3);">
                                    <div style="font-size: 16px; font-weight: 700; margin-right: 12px;">{{ event?.name }}</div>
                                    <div style="font-size: 12px; letter-spacing: 0.1em;">{{ event?.time }}</div>
                                </div>
                            </div>
                        </div>
                        <div style="text-align: center; margin-top: 20px;">
                            <NuxtLink class="button" to="/events" style="background-color: var(--color1); color: white;">
                                <div>所有活動／課程</div>
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <section style="padding: 120px 0px; background: var(--color2);">
            <div style="max-width: 1000px; width: 90%; margin: auto;" class="committee-list">
                <div style="font-size: 15px; color: var(--color1); letter-spacing: 0.2em; font-weight: 600;">社團幹部</div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(170px, 1fr)); gap: 10px;" v-if="data?.contents?.length">
                    <div class="committee" v-for="committee in data?.contents">
                        <img :src="committee?.avatar?.url ?? '/gdc-character.png'" alt="" draggable="false">
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
        height: 800px;
        background-image: url('/logo_large.png');
        background-size: auto 60%;
        background-repeat: no-repeat;
        background-position: 55%center;
    }

    header > h1 {
        text-align: center;
        font-size: 45px;
        font-weight: 400;
        letter-spacing: 0.2em;
        color: var(--color5);
        margin: 0;
        margin-top: 12px;
        line-height: 1.2;
    }

    header > h1 > span {
        font-size: 15px;
        font-weight: 700;
        letter-spacing: 0.8em;
    }

    #bg {
        background-image: url('/images.png');
        background-size: auto 90%;
        background-repeat: no-repeat;
        background-position: center;
        position: absolute;
        width: 100%;
        height: 100%;
    }

    .window {
        position: relative;
        max-width: 480px;
        color: var(--color3);
        border: 1px solid var(--color2);
        background-color: #ffffffaa;
        backdrop-filter: blur(4px);
        letter-spacing: 0.05em;
        margin: 60px 16px;
        line-height: 1.8;
        font-size: 13px;
        box-shadow: 4px 4px var(--color2);
        border-radius: 8px;
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
        margin-bottom: 12px;
        border-radius: 8px;
    }

    .about-pictures p {
        font-size: 13px;
        letter-spacing: 0.1em;
        color: var(--color3);
    }

    .about-button {
        color: white;
        text-decoration: none;
        padding: 16px;
        background: var(--color3);
        border-radius: 60px;
        font-size: 24px;
    }

    .news-events {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 40px;
    }
    
    .committee-list {
        display: grid;
        grid-template-columns: 240px 1fr;
        gap: 20px;
    }

    .committee {
        width: 100%;
        overflow: hidden;
        color: var(--color3);
        background-color: white;
        display: flex;
        border-radius: 8px;
    }

    .committee > img {
        width: 56px;
        height: 56px;
        object-fit: cover;
        background-color: var(--color3);
    }

    .split-content {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    @media (max-width: 800px) {
        #bg {
            background-position: right center;
        }

        .about-pictures {
            grid-template-columns: 1fr;
        }

        .split-content {
            display: block;
        }

        .images {
            opacity: 0.2;
        }

        .news-events, .committee-list {
            grid-template-columns: 1fr;
        }
    }
</style>