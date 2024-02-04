<template>
    <div>
        <div class="flex items-center justify-between ">
            <div class="text-[24px]">{{ title }}</div>
            <input type="text" placeholder="Search..."
            class="border rounded-md py-1 px-2"
            />
        </div>
        <slot />
    </div>
</template>

<script>
    export default {
        props: {
            title: {
                type: String,
                // required: true,
                default: 'Page Title'
            }
        }
    }
</script>