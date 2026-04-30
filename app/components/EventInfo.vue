<script setup>
    const props = defineProps(['event'])
</script>

<template>
    <article class="event">
        <div style="position: relative;">
            <img :src="props.event?.image?.url ?? '/icon.png'" alt="" draggable="false" :style="props.event?.ended? { filter: 'grayScale(1)', opacity: 0.5 } : {}">
            <div style="display: flex; flex-wrap: wrap; align-items: center; background: linear-gradient(0deg, #000000aa 30%, transparent 100%); color: white; position: absolute; width: 100%; bottom: 0; padding: 32px 16px 16px 16px; box-sizing: border-box;">
                <div style="font-size: 16px; font-weight: 700; margin-right: 12px;">{{ props.event?.name }}</div>
                <div style="font-size: 12px; letter-spacing: 0.1em;">{{ props.event?.time }}</div>
            </div>
            <div class="tag" :style="props.event?.ended? { backgroundColor: 'var(--color3)' } : { backgroundColor: 'var(--color5)' }">{{ props.event?.type[0] }}</div>
        </div>
        <div class="event-info">
            <div v-if="props.event?.teacher" style="font-weight: 700; color: var(--color3);">講師</div>
            <div v-if="props.event?.teacher">{{ props.event?.teacher }}</div>
            <div v-if="props.event?.place" style="font-weight: 700; color: var(--color3);">地點</div>
            <div v-if="props.event?.place">{{ props.event?.place }}</div>
            <div v-if="props.event?.students" style="font-weight: 700; color: var(--color3);">學員</div>
            <div v-if="props.event?.students">{{ props.event?.students }}</div>
            <div v-if="props.event?.form" style="font-weight: 700; color: var(--color3);">形式</div>
            <div v-if="props.event?.form">{{ props.event?.form }}</div>
            <div v-if="props.event?.week" style="font-weight: 700; color: var(--color3);">週次</div>
            <div v-if="props.event?.week">{{ props.event?.week }}</div>
            <div v-if="props.event?.feature" style="font-weight: 700; color: var(--color3);">特色</div>
            <div v-if="props.event?.feature">{{ props.event?.feature }}</div>
        </div>
        <div v-if="props.event?.description" class="event-description">
            <div>{{ props.event?.description }}</div>
        </div>
        <div v-if="props.event?.link && !props.event?.ended" style="padding: 16px; text-align: center;">
            <NuxtLink class="button" target="_blank" :to="props.event?.link">
                <div>報名連結</div>
            </NuxtLink>
        </div>
    </article>
</template>

<style>
    .event {
        position: relative;
        overflow: hidden;
        border: solid 1px var(--color2);
        border-radius: 8px;
        background-color: white;
    }

    .event img {
        width: 100%;
        aspect-ratio: 2;
        display: block;
        object-fit: cover;
    }

    .event-info {
        padding: 16px;
        display: grid;
        grid-template-columns: 32px 1fr;
        gap: 8px;
        letter-spacing: 0.05em;
        font-size: 12px;
        white-space: pre-wrap;
    }

    .event-description {
        border-top: 1px solid var(--color2);
        padding: 16px;
        letter-spacing: 0.05em;
        font-size: 12px;
        white-space: pre-wrap;
    }

    .tag {
        position: absolute;
        top: 0px;
        right: 0px;
        color: white;
        font-size: 12px;
        padding: 4px 16px;
        letter-spacing: 0.1em;
        font-weight: 600;
        text-align: center;
        width: 200px;
        transform: translate(75px, 15px) rotate(30deg);
    }
</style>