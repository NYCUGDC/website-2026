<script setup>
    const { params } = useRoute()
    const { data } = await useMicroCMSGetList({
        endpoint: "articles",
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
        title: data?.value?.contents[0]?.title,
        ogTitle: data?.value?.contents[0]?.title
    })
</script>

<template>
    <section style="margin: 200px 0px;">
        <div style="max-width: 1000px; width: 90%; margin: auto;">
            <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">社團文章</div>
            <h1 style="color: var(--color5); margin-top: 8px;">{{ data?.contents[0]?.title }}</h1>
                <p style="color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">作者</span>{{ data?.contents[0]?.author }}</p>
            <ClientOnly>
                <p style="color: var(--color3);"><span style="font-weight: 600; margin-right: 12px;">發佈時間</span>{{ convertDate(data?.contents[0]?.publishedAt) }}</p>
            </ClientOnly>
            <div class="articles-content" v-html="data?.contents[0]?.content"></div>
        </div>
    </section>
</template>

<style>
    .articles-content {
        margin: 100px 0px;
        line-height: 1.8;
        padding: 12px 20px;
        border-radius: 20px;
        background-color: white;
        border: 1px solid var(--color2);
    }

    .articles-content table {
        border-collapse: collapse;
    }

    .articles-content tr, td {
        border: 1px solid var(--color2);
        padding: 8px;
    }

    .articles-content blockquote {
        padding: 8px;
        border-radius: 8px;
        border: 1px solid var(--color2);
        color: var(--color3);
    }

    .articles-content p {
        margin-block-start: 0px;
        margin-block-end: 0px;
    }

    .articles-content p + p {
        margin-block-start: 1em;
        margin-block-end: 0px;
    }

    .articles-content pre {
        color: var(--color2);
        background-color: var(--color1);
        padding: 8px;
        border-radius: 8px;
        overflow-x: scroll;
    }

    .articles-content a {
        color: var(--color4);
    }

    @media (max-width: 800px) {
        .articles-content {
            font-size: 13px;
        }
    }
</style>