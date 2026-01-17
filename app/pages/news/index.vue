<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "news" }, { key: 'news' })

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleString('zh-TW')
    }

    useSeoMeta({
        title: '最新消息'
    })
</script>

<template>
    <section style="margin: 200px 0px;">
        <div style="max-width: 1200px; width: 90%; margin: auto;">
            <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">最新消息</div>
            <h1 style="color: var(--color5); margin-top: 8px;">News</h1>
            <p style="color: var(--color3);">關於社團近期的一些活動事項與重要公告</p>
            <div class="news" v-if="data?.contents?.length" style="margin-top: 100px;">
                <NuxtLink v-for="news in data?.contents" :to="'/news/' + news?.slug" style="text-decoration: unset; color: unset; position: relative;">
                    <article>
                        <h2 style="margin: 0 0 12px 0; font-size: 18px; font-weight: 600;">{{ news?.title }}</h2>
                        <ClientOnly>
                            <div style="font-size: 12px; color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">發布時間</span>{{ convertDate(news?.publishedAt) }}</div>
                        </ClientOnly>
                        <div style="position: absolute; height: 100%; width: 120px; background-image: url('/gdc-character.png'); background-size: cover; top: 0; right: 20px; filter: invert(1); opacity: 0.1;"></div>
                    </article>
                </NuxtLink>
            </div>
        </div>
    </section>
</template>

<style>
</style>