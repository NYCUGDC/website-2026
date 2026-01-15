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
        return date.toLocaleDateString('zh-TW')
    }

    useSeoMeta({
        title: data?.value?.contents[0]?.title
    })
</script>

<template>
    <section style="margin: 100px 0px;">
        <div style="max-width: 1200px; width: 90%; margin: auto;">
            <h1 style="color: var(--color5);">{{ data?.contents[0]?.title }}</h1>
            <p style="color: var(--color3);">{{ convertDate(data?.contents[0]?.date) }}</p>
            <div class="news-content" v-html="data?.contents[0]?.content"></div>
        </div>
    </section>
</template>

<style>
    .news-content {
        margin-top: 60px;
        margin-bottom: 200px;
        line-height: 1.8;
    }

    @media (max-width: 800px) {
        .news-content {
            font-size: 13px;
        }
    }
</style>