<template>
    <div class="img-wrapper" :style="style">
        <slot name="image-container">
            <a :href="href" :data-href="dataHref">
                <transition name="fade">
                    <img v-show="showImage" :src="full" class="reveal" :alt="alt" :data-srcset="dataSrcSet"
                         :data-sizes="dataSizes" @load="onImageLoaded()" @error="onImageError()">
                </transition>
            </a>
        </slot>

        <transition name="fade-out">
            <div v-if="showSpinner" class="sub-container"
                 :style="{'width': spinnerSize, 'height': spinnerSize, 'opacity': showSpinner ? 1 : 0}">
                <svg class="circular" :style="{'width': spinnerSize, 'height': spinnerSize}" viewBox="25 25 50 50">
                    <circle class="path" cx="50" cy="50" r="20" fill="none" stroke-width="2"
                            stroke-miterlimit="10"/>
                </svg>
            </div>
        </transition>

        <div class="sub-container" :style="emptyStyle">
            <span class="label">{{ emptyLabel }}</span>
        </div>
    </div>
</template>

<script lang="ts">
import {Component, Prop, Vue} from 'vue-property-decorator';

@Component
export default class VueImage extends Vue {

    // ------------------------------------------------------------------------------
    //  PROPERTIES
    // ------------------------------------------------------------------------------

    @Prop({default: ''}) private link!: string;
    @Prop() private full!: string;
    @Prop({default: ''}) private preview!: string;
    @Prop({default: ''}) private alt!: string;
    @Prop({default: ''}) private dataSrcSet!: string;
    @Prop({default: ''}) private dataSizes!: string;
    @Prop({default: '64px'}) private spinnerSize!: string;
    @Prop({default: '120px'}) private width!: string;
    @Prop({default: 'auto'}) private height!: string;
    @Prop({default: () => ({})}) private css!: object;
    @Prop({default: 'No image found!'}) private emptyLabel!: string;

    // ------------------------------------------------------------------------------
    //  DATA
    // ------------------------------------------------------------------------------

    private loaded: boolean = false;
    private error: boolean = false;

    // ------------------------------------------------------------------------------
    //  COMPUTED
    // ------------------------------------------------------------------------------

    get href(): string {
        return this.link.length > 0 ? this.link : this.full;
    }

    get dataHref(): string {
        return this.link.length > 0 ? this.full : '';
    }

    get style(): object {
        let style = {
            backgroundColor: '#FFFFFF',
            maxWidth: this.width,
            height: this.height,
        };

        if (this.hasPreviewImage) {
            style = Object.assign(style, {backgroundImage: 'url(' + this.preview + ')'});

            if (this.error) {
                style = Object.assign(style, {
                    border: '1px solid #dee2e6',
                    borderRadius: '3px',
                });
            }
        } else {
            style = Object.assign(style, {
                border: '1px solid #dee2e6',
                borderRadius: '3px',
            });
        }

        return Object.assign(style, this.css);
    }

    get emptyStyle(): object {
        return {
            'background-color': '#FFFFFF',
            'opacity': this.showError ? 0.85 : 0,
            '-webkit-transition': 'opacity 1000ms linear',
            '-ms-transition': 'opacity 1000ms linear',
            'transition': 'opacity 1000ms linear',
        };
    }

    get hasPreviewImage(): boolean {
        return this.preview !== '';
    }

    get showImage(): boolean {
        return this.loaded && !this.error;
    }

    get showSpinner(): boolean {
        return !this.hasPreviewImage && !this.loaded;
    }

    get showError(): boolean {
        return this.loaded && this.error;
    }


    // ------------------------------------------------------------------------------
    //  METHODS
    // ------------------------------------------------------------------------------

    private onImageLoaded(): void {
        this.loaded = true;
    }

    private onImageError(): void {
        this.loaded = true;
        this.error = true;
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .img-wrapper {
        position: relative;
        display: block;
        overflow: hidden;
        outline: none;
        background-size: cover;
        background-position: center;
        width: auto;
    }

    .img-wrapper img {
        display: block;
        width: 100%;
        max-width: none;
        height: auto;
        border: 0 none;
        top: 0;
        left: 0;
    }

    @keyframes reveal {
        0% {
            transform: scale(1.05);
            opacity: 0;
        }
        100% {
            transform: scale(1);
            opacity: 1;
        }
    }

    @keyframes preview {
        0% {
            opacity: 1;
        }
        100% {
            opacity: 0;
        }
    }

    .fade-enter-active {
        transition: opacity 1s ease-in-out;
    }

    .fade-enter-to {
        opacity: 1;
    }

    .fade-enter {
        opacity: 0;
    }

    .fade-out-leave-active {
        transition: opacity 250ms ease-in-out;
    }

    .fade-out-leave-to {
        opacity: 0;
    }

    .fade-out-leave {
        opacity: 1;
    }

    .disable-horizontal-center {
        top: unset !important;
        bottom: unset !important;
    }

    .disable-vertical-center {
        left: unset !important;
        right: unset !important;
    }

    .sub-container {
        display: flex;
        align-items: center;
        position: absolute;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
        opacity: 0;
    }

    .circular {
        animation: rotate 2s linear infinite;
        transform-origin: center center;
        display: block;
        margin: 0 auto;
    }

    .path {
        stroke-dasharray: 1, 200;
        stroke-dashoffset: 0;
        animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
        stroke-linecap: round;
    }

    @keyframes rotate {
        100% {
            transform: rotate(360deg);
        }
    }

    @keyframes dash {
        0% {
            stroke-dasharray: 1, 200;
            stroke-dashoffset: 0;
        }
        50% {
            stroke-dasharray: 89, 200;
            stroke-dashoffset: -35px;
        }
        100% {
            stroke-dasharray: 89, 200;
            stroke-dashoffset: -124px;
        }
    }

    @keyframes color {
        100%,
        0% {
            stroke: #d62d20;
        }
        40% {
            stroke: #0057e7;
        }
        66% {
            stroke: #008744;
        }
        80%,
        90% {
            stroke: #ffa700;
        }
    }

    .label {
        margin: 0 auto;
    }
</style>
