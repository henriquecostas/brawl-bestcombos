<template>

        <div class="character-image">
            <slot
             :width='image.size.width'
             :height='image.size.height'
            >
            </slot>
        </div>
    
</template>

<script>
export default {
    name:'CharacterImage',
    props:[
        'url', 
        'description', 
        'width',
        'height'
    ],

    data() {
        return {
            image:{
                size:{
                    width: '480px',
                    height: '540px'
                }
            }
        }
    }
}
</script>

<style scoped>
    .character-image{
        position: absolute;

        width: 480px;
        height: 540px;
        z-index: 4;
    }

    .character-image img{
        width: 100%;
        height: 100%;
    }

    @media (max-width: 390px) {
        .character-image {
            display: none;
        }

        .character-image img{
            display: none;
        }
    }

</style>