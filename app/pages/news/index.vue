<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "news" }, { key: 'news' })

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleDateString('zh-TW')
    }

    useSeoMeta({
        title: '最新消息'
    })
</script>

<template>
    <section style="margin: 100px 0px;">
        <div style="max-width: 1200px; width: 90%; margin: auto;">
            <div style="font-size: 15px; color: var(--color5); letter-spacing: 0.2em; font-weight: 700;">最新消息</div>
            <h1 style="color: var(--color5);">News</h1>
            <p style="color: var(--color3);">關於社團近期的一些活動事項與重要公告</p>
            <div class="news" v-if="data?.contents?.length">
                <NuxtLink v-for="news in data?.contents" :to="'/news/' + news?.slug" style="text-decoration: unset; color: unset; position: relative;">
                    <article>
                        <h2 style="margin: 0 0 12px 0; font-size: 18px; font-weight: 600;">{{ news?.title }}</h2>
                        <div style="font-size: 12px; color: var(--color3);">{{ convertDate(news?.date) }}</div>
                        <div style="position: absolute; height: 100%; width: 120px; background-image: url('/gdc-character.png'); background-size: cover; top: 0; right: 20px; filter: invert(1); opacity: 0.1;"></div>
                    </article>
                </NuxtLink>
            </div>
        </div>
    </section>
</template>

<style>
    .news {
        margin-top: 100px;
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
</style>