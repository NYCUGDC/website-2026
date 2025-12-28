<script setup>
    const { data } = await useMicroCMSGetList({ endpoint: "events" }, { key: 'events' })

    useSeoMeta({
        title: '活動與課程'
    })
</script>

<template>
    <div>
        <section style="margin: 100px 0px;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <div style="font-size: 15px; color: var(--color5); letter-spacing: 0.2em; font-weight: 700;">活動與課程</div>
                <h1 style="color: var(--color5);">Events & Course</h1>
                <p style="color: var(--color3);">此處列出了 GDC 社團近期舉辦的課程與活動，歡迎大家踴躍參加！</p>
                <h2 style="margin-top: 60px; color: var(--color3);">本學期</h2>
                <div class="events" v-if="data?.contents?.length">
                    <article class="event" v-for="event in data?.contents?.filter(e => !e?.ended)">
                        <div style="position: relative;">
                            <img :src="event?.image?.url ?? '/icon.png'" alt="" draggable="false">
                            <div style="display: flex; flex-wrap: wrap; align-items: center; background-color: #00000080; color: white; position: absolute; width: 100%; bottom: 0; padding: 16px;">
                                <div style="font-size: 16px; font-weight: 700; margin-right: 12px;">{{ event?.name }}</div>
                                <div style="font-size: 12px; letter-spacing: 0.1em;">{{ event?.time }}</div>
                            </div>
                        </div>
                        <div class="event-info">
                            <div v-if="event?.teacher" style="font-weight: 700; color: var(--color3);">講師</div>
                            <div v-if="event?.teacher">{{ event?.teacher }}</div>
                            <div v-if="event?.place" style="font-weight: 700; color: var(--color3);">地點</div>
                            <div v-if="event?.place">{{ event?.place }}</div>
                            <div v-if="event?.students" style="font-weight: 700; color: var(--color3);">學員</div>
                            <div v-if="event?.students">{{ event?.students }}</div>
                            <div v-if="event?.form" style="font-weight: 700; color: var(--color3);">形式</div>
                            <div v-if="event?.form">{{ event?.form }}</div>
                            <div v-if="event?.week" style="font-weight: 700; color: var(--color3);">週次</div>
                            <div v-if="event?.week">{{ event?.week }}</div>
                            <div v-if="event?.feature" style="font-weight: 700; color: var(--color3);">特色</div>
                            <div v-if="event?.feature">{{ event?.feature }}</div>
                            <div v-if="event?.description" style="font-weight: 700; color: var(--color3);">內容</div>
                            <div v-if="event?.description">{{ event?.description }}</div>
                        </div>
                    </article>
                    <div></div>
                </div>
                <h2 style="margin-top: 60px; color: var(--color3);">已結束</h2>
                <div class="events" v-if="data?.contents?.length">
                    <article class="event" v-for="event in data?.contents?.filter(e => e?.ended)">
                        <div style="position: relative;">
                            <img :src="event?.image?.url ?? '/icon.png'" alt="" style="filter: grayscale(1); opacity: 0.5;" draggable="false">
                            <div style="display: flex; flex-wrap: wrap; align-items: center; background-color: #00000080; color: white; position: absolute; width: 100%; bottom: 0; padding: 16px;">
                                <div style="font-size: 16px; font-weight: 700; margin-right: 12px;">{{ event?.name }}</div>
                                <div style="font-size: 12px; letter-spacing: 0.1em;">{{ event?.time }}</div>
                            </div>
                        </div>
                        <div class="event-info">
                            <div v-if="event?.teacher" style="font-weight: 700; color: var(--color3);">講師</div>
                            <div v-if="event?.teacher">{{ event?.teacher }}</div>
                            <div v-if="event?.place" style="font-weight: 700; color: var(--color3);">地點</div>
                            <div v-if="event?.place">{{ event?.place }}</div>
                            <div v-if="event?.students" style="font-weight: 700; color: var(--color3);">學員</div>
                            <div v-if="event?.students">{{ event?.students }}</div>
                            <div v-if="event?.form" style="font-weight: 700; color: var(--color3);">形式</div>
                            <div v-if="event?.form">{{ event?.form }}</div>
                            <div v-if="event?.week" style="font-weight: 700; color: var(--color3);">週次</div>
                            <div v-if="event?.week">{{ event?.week }}</div>
                            <div v-if="event?.feature" style="font-weight: 700; color: var(--color3);">特色</div>
                            <div v-if="event?.feature">{{ event?.feature }}</div>
                            <div v-if="event?.description" style="font-weight: 700; color: var(--color3);">內容</div>
                            <div v-if="event?.description">{{ event?.description }}</div>
                        </div>
                    </article>
                    <div></div>
                </div>
            </div>
        </section>
        <section style="background-color: var(--color2); margin-top: 90px; padding: 60px 0 100px 0;">
            <div style="max-width: 1200px; width: 90%; margin: auto;">
                <h2 style="font-size: 40px; color: var(--color3);">FAQ</h2>
                <p style="color: var(--color4); font-weight: 700; font-size: 13px;">要怎麼加入 GDC 呢？</p>
                <p>填寫入社表單、並繳交 300元社費即可！<br>（可於社博繳交社費、其餘繳交方式詳見表單）</p>
                <br>
                <p style="color: var(--color4); font-weight: 700; font-size: 13px;">完全沒碰過程式或建模，門檻會不會很高？</p>
                <p>每學期社課皆會有「基礎」、「進階」的課程，基礎課程將會以零程式、建模基礎來授課。選擇適合自己的課程吧！</p>
                <br>
                <p style="color: var(--color4); font-weight: 700; font-size: 13px;">對社課有興趣，但當天有課無法參加><</p>
                <p>課程講義、影片紀錄等資源都會保存在Discord的社員頻道中，課後複習完全ok！</p>
            </div>
        </section>
    </div>
</template>

<style>
    .events {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
        gap: 16px;
    }

    .event {
        position: relative;
        overflow: hidden;
        border-radius: 12px;
        border: solid 1px var(--color2);
    }

    .event img {
        width: 100%;
        aspect-ratio: 2.3;
        display: block;
        object-fit: cover;
    }

    .event-info {
        padding: 24px;
        display: grid;
        grid-template-columns: 40px 1fr;
        gap: 10px;
        letter-spacing: 0.05em;
        font-size: 12px;
        white-space: pre-wrap;
    }

    @media (max-width: 800px) {
        .events {
            grid-template-columns: 1fr;
        }
    }
</style>