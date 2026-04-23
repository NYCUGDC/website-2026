<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "articles", queries: { limit: 50 } }, { key: 'articles' })

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleString('zh-TW')
    }

    useSeoMeta({
        title: '社團文章'
    })
</script>

<template>
    <section style="margin: 200px 0px;">
        <div style="max-width: 1000px; width: 90%; margin: auto;">
            <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">社團文章</div>
            <h1 style="color: var(--color5); margin-top: 8px;">Articles</h1>
            <p style="color: var(--color3);">來自社團成員分享，遊戲開發相關技術的介紹與教學文章</p>
            <div class="articles" v-if="data?.contents?.length" style="margin-top: 100px;">
                <NuxtLink v-for="article in data?.contents" :to="'/articles/' + article?.slug" style="text-decoration: unset; color: unset; position: relative;">
                    <article class="article">
                        <div>
                            <img :src="article?.image?.url ?? '/gdc-character.png'" alt="" style="width: 100%; aspect-ratio: 2; object-fit: cover; border-bottom: solid 2px var(--color2); background-color: var(--color3);">
                        </div>
                        <div style="margin: 12px;">
                            <h2 style="margin: 0 0 12px 0; font-size: 18px; font-weight: 600;">{{ article?.title }}</h2>
                                <div style="font-size: 12px; color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">作者</span>{{ article?.author }}</div>
                            <ClientOnly>
                                <div style="font-size: 12px; color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">發布時間</span>{{ convertDate(article?.publishedAt) }}</div>
                            </ClientOnly>
                        </div>
                    </article>
                </NuxtLink>
            </div>
        </div>
    </section>
</template>

<style>
</style>