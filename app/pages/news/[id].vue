<script setup>
    const { params } = useRoute()
    const { data } = await useMicroCMSGetList({
        endpoint: "news",
        queries: {
            limit: 1,
            filters: 'slug[equals]' + params.id
        }
    }, { key: params.id })

    function convertDate(text) {
        const date = new Date(text)
        return date.toLocaleString('zh-TW')
    }

    useSeoMeta({
        title: data?.value?.contents[0]?.title
    })
</script>

<template>
    <section style="margin: 200px 0px;">
        <div style="max-width: 1200px; width: 90%; margin: auto;">
            <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">最新消息</div>
            <h1 style="color: var(--color5); margin-top: 8px;">{{ data?.contents[0]?.title }}</h1>
            <ClientOnly>
                <p style="color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">發佈時間</span>{{ convertDate(data?.contents[0]?.publishedAt) }}</p>
            </ClientOnly>
            <div class="news-content" v-html="data?.contents[0]?.content"></div>
        </div>
    </section>
</template>

<style>
    .news-content {
        margin: 100px 0px;
        line-height: 1.8;
        padding: 12px 20px;
        border-radius: 20px;
        background-color: white;
        border: 1px solid var(--color2);
    }

    @media (max-width: 800px) {
        .news-content {
            font-size: 13px;
        }
    }
</style>