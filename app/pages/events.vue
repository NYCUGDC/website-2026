<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "events" }, { key: 'events' })

    useSeoMeta({
        title: '活動與課程'
    })
</script>

<template>
    <div>
        <section style="margin: 200px 0px;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <div style="font-size: 12px; color: var(--color5); letter-spacing: 0.2em; font-weight: 600;">活動與課程</div>
                <h1 style="color: var(--color5); margin-top: 8px;">Events & Course</h1>
                <p style="color: var(--color3);">此處列出了 GDC 社團近期舉辦的課程與活動，歡迎大家踴躍參加！</p>
                <h2 style="margin-top: 60px; color: var(--color3);">本學期</h2>
                <div class="events" v-if="data?.contents?.length">
                    <div v-if="!data?.contents?.filter(e => !e?.ended)?.length" style="display: flex; align-items: center; justify-content: center; color: var(--color3); background-color: var(--color2); padding: 20px;">
                        活動準備中，敬請期待！
                    </div>
                    <EventInfo v-for="event in data?.contents?.filter(e => !e?.ended)" :event="event" />
                    <div></div>
                    <div></div>
                </div>
                <h2 style="margin-top: 60px; color: var(--color3);">已結束</h2>
                <div class="events" v-if="data?.contents?.length">
                    <EventInfo v-for="event in data?.contents?.filter(e => e?.ended)" :event="event" />
                    <div></div>
                    <div></div>
                </div>
            </div>
        </section>
        <section style="background-color: var(--color2); margin-top: 90px; padding: 60px 0 100px 0;">
            <div style="max-width: 1200px; width: 90%; margin: auto; line-height: 1.5; text-align: center;">
                <h2 style="font-size: 40px; color: var(--color3);">FAQ</h2>
                <p style="color: var(--color4); font-weight: 600; font-size: 13px; letter-spacing: 0.1em;">要怎麼加入 GDC 呢？</p>
                <p>填寫入社表單、並繳交 300 元社費即可！<br>（可於社博繳交社費、其餘繳交方式詳見表單）</p>
                <br>
                <p style="color: var(--color4); font-weight: 600; font-size: 13px; letter-spacing: 0.1em;">完全沒碰過程式或建模，門檻會不會很高？</p>
                <p>每學期社課皆會有「基礎」、「進階」的課程，基礎課程將會以零程式、建模基礎來授課。選擇適合自己的課程吧！</p>
                <br>
                <p style="color: var(--color4); font-weight: 600; font-size: 13px; letter-spacing: 0.1em;">對社課有興趣，但當天有課無法參加><</p>
                <p>課程講義、影片紀錄等資源都會保存在 Discord 的社員頻道中，課後複習完全ok！</p>
            </div>
        </section>
    </div>
</template>

<style>
    .events {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
        gap: 16px;
    }

    @media (max-width: 800px) {
        .events {
            grid-template-columns: 1fr;
        }
    }
</style>