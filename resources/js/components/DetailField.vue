<template>
    <div class="flex flex-col md:flex-row -mx-6 px-6 py-2 md:py-0 space-y-2 md:space-y-0 border-t border-gray-100 dark:border-gray-700">

        <div class="md:w-1/4 md:py-3">
            <h4 class="font-bold md:font-normal">
                <span>{{ field.name }}</span>
            </h4>
        </div>
        <div class="md:w-3/4 md:py-3">
            <div>
                <iframe v-if="showIframe" :width="width" :height="height" :class="classes" :style="style" :src="src" :srcdoc="computedSrcdoc"></iframe>
                <p v-else>—</p>
            </div>
        </div>

    </div>
</template>

<script>
export default {

    props: ['resource', 'resourceName', 'resourceId', 'field'],

    data: () => ({
        width: "100%",
        height: 600,
        classes: null,
        style: null,
        showIframe: false,
        src: null,
    }),
    computed: {
        computedSrcdoc() {
            // Check if src is null or empty, and return content as srcdoc if needed
            if (!this.src && this.field.value) {
                this.showIframe = true;
                return this.field.value;
            }
            return null; // No srcdoc if src is not null or empty
        }
    },
    mounted: function () {

        // Set the width
        if (this.field.hasOwnProperty('width')) {
            this.width = this.field.width;
        }

        // Set the height
        if (this.field.hasOwnProperty('height')) {
            this.height = this.field.height;
        }

        // Set the classes
        if (this.field.hasOwnProperty('classes')) {
            this.classes = this.field.classes;
        }

        // Set the style
        if (this.field.hasOwnProperty('style')) {
            this.style = this.field.style;
        }

        // Only show iframe if we have a value or src
        if (this.field.hasOwnProperty('src')) {
            this.src = this.field.src;
            this.showIframe = true;
        }
    }
}
</script>