<template>
  <div id="app">

    <VideoPanel>
        <video
            class="video" 
            src="/video/replay-cross.mp4"
            autoplay 
            muted
            loop   
            v-on:click="watchToggle"  
        >
        </video>
    </VideoPanel>

    <div class="colorize"></div>

    <VideoPanelTitle 
        :name='game.character.name'
        :title='game.description.title'
        :subtitle='game.description.subtitle'
    >
    </VideoPanelTitle>

    <div class='static-bar'>
        <img class='game-logo' 
            :src='game.image.src' 
            :alt='game.image.alt'
        />
    </div>

    <div class="half-panel">
        <CharacterImage>
            <img :src='game.character.image' :alt='game.character.description' />
        </CharacterImage>
    </div>
    <div class="panel">
        <SlideVideo>
            <li 
                v-for='video in game.character.video' 
                :key='video.id'
                class="slide-item"
            >
                <a v-bind:href="video.src">
                    <img :src="video.thumb" />
                </a>
            </li>
        </SlideVideo> 
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import CharacterImage from './components/shared/CharacterImage/CharacterImage.vue';
import VideoPanel from './components/shared/VideoPanel/VideoPanel.vue';
import VideoPanelTitle from './components/shared/VideoPanelTitle/VideoPanelTitle.vue';
import SlideVideo from './components/shared/SlideVideo/SlideVideo.vue';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    CharacterImage,
    VideoPanel,
    VideoPanelTitle,
    SlideVideo
  },

  data(){
        return {
            game:{
                description: {
                    title: "TOP 5",
                    subtitle: "BEST COMBOS"
                },

                image:{
                    src: "/img/brawhalla-logo.png",
                    alt: "Logo do jogo Brawhalla"
                },

                character: {
                    name: 'CROSS',
                    image: '/img/cross_img1.png',
                    description: 'Imagem do Cross',
                    video:[
                        {
                            src: "/public/video/replay-cross.mp4",
                            thumb: "/img/thumb/thumb1.png"
                        },
                        {
                            src: "/video/replay-cross.mp4",
                            thumb: "/img/thumb/thumb2.png"
                        },
                        {
                            src: "/video/replay-cross.mp4",
                            thumb: "/img/thumb/thumb3.png"
                        },
                        {
                            src: "/video/replay-cross.mp4",
                            thumb: "/img/thumb/thumb1.png"
                        },
                        {
                            src: "/video/replay-cross.mp4",
                            thumb: "/img/thumb/thumb1.png"
                        }                   
                    ],
                },    
            }
        }
    },

    methods: {
        watchToggle: function() {
            let container = document.querySelector('.video-display');
            let video = container.querySelector('.video-display .video');

            if (video.classList.contains('watch')) {
                video.classList.remove('watch')
                container.classList.remove('watch')
            } else {
                video.classList.add('watch')
                container.classList.add('watch')
                video.setAttribute('v-on:click','watchToggle')
            }
        }
    }
}
</script>

<style>

* {
        margin: 0px;
        padding:  0px;
        box-sizing: border-box;

    }

    #app {

        height: 100%;
        width: 100%;

        max-width: 1440px;
        max-height: 720px;

        display: flex;

        background-color: #1E1E1E;    
        border-radius: 8px;
        border: 1px solid #193c4b;

    }

    html {

        width: 100vw;
        height: 100vh;
        margin: 0 auto;
        
    }

    body {

        width: 100%;
        height: 100%;
        
        margin: 0 auto;
        
        display: flex;
        justify-content: center;
        align-items: center;
        
        background-color: #182429;
        overflow: hidden;

    }

    .static-bar {
        z-index: 1;

        display: flex;
        justify-content: center;
        align-items: center;
        
        width: 20%;
        
        background: linear-gradient(180deg, #182429 14.9%, #193C4B 82.08%);
        border-radius: 0px 8px 8px 0px;
    }

    .game-logo {
        min-width: 80%;
        padding: 20px;
    }

    .colorize {
        background: rgba(25, 60, 75, 0.27);
        width: 100%;
        height: 100%;
        position: absolute;
        max-width: 1440px;
        max-height: 720px;
        border-radius: 8px;
    }

    .panel {
        width: 100%;
        height: 100%;
        position: absolute;
        max-width: 1440px;
        max-height: 720px;
        border-radius: 8px;
    }

    .half-panel {
        width: 100%;
        height: 100%;
        position: absolute;
        max-width: 1222px;
        max-height: 720px;
        display: flex;
        flex-direction: row-reverse;
        align-items: center;
        border-radius: 8px;
    }
    
    @media (max-width: 360px) {
        .static-bar{
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 60px;
        }

        .game-logo {
            height: 40px;
            width: auto;
            min-width: 0;
            padding: 0;
        }
    }   
</style>
