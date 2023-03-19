<template class="container">
        <div class="slide-container">

            <!-- <div class="arrow-previous control">
                <img
                    src="/svg/arrow-left.svg"
                    alt="Passar slide para esquerda"
                />
            </div> -->

            <div class="slide-content">
                <ul class="slide-list">
                    <slot class="slide-item"></slot>
                </ul>
            </div>

            <!-- <div class="arrow-next control">
                <img 
                    src="/svg/arrow-right.svg"
                    alt="Passar slide para direita"
                />
            </div> -->

            <div class="select-container">
                <div class="arrow-previous control">
                    <img
                        src="/svg/arrow-left.svg"
                        alt="Passar slide para esquerda"
                    />
                </div>
                <div class="arrow-next control">
                    <img 
                        src="/svg/arrow-right.svg"
                        alt="Passar slide para direita"
                    />
                </div>
            </div>

        </div>
</template>

<script>

    export default { 
        data() {
            return {

            }
        },

        mounted () {
            const controls = document.querySelectorAll(".control");
            let items = document.querySelectorAll('.slide-item');    
            
            const selectContainer = document.querySelector('.select-container');
            let selectItems = []

            items.forEach(() => {
                let select = document.createElement('div')
                selectContainer.appendChild(select)
                select.classList.add('select-item')
                selectItems.push(select)
            })

            let slideItem = {
                current: 0,
                previous: 0,
                next: 0,
                max: items.length
            }

            items[slideItem.current].classList.add('active');
            selectItems[slideItem.current].classList.add('selected');

            controls.forEach(control => {
                control.addEventListener('click', () => {
                    const isRight = control.classList.contains('arrow-next')

                    if (isRight) {
                        slideItem.current += 1;
                    } else {
                        slideItem.current -= 1;
                    }

                    if (slideItem.current >= slideItem.max) {
                        slideItem.current = 0;
                    }

                    if (slideItem.current < 0) {
                        slideItem.current = slideItem.max - 1;
                    }
                    
                    items.forEach((item) => 
                        item.classList.remove('active')
                    );
                        
                    selectItems.forEach((select) => 
                        select.classList.remove('selected')
                    );

                    items[slideItem.current].scrollIntoView({
                        inline: "center",
                        behavior: "smooth"
                    })
                
                    items[slideItem.current].classList.add('active');
                    let elementoLink = items[slideItem.current].querySelector('a')

                    let video = document.querySelector('video')

                    video.src = elementoLink.href
                    selectItems[slideItem.current].classList.add('selected');


                })
            })

            selectItems.forEach(select => {
                select.addEventListener('click', () => {
                    const isSelected = select.classList.contains('selected');

                    if (isSelected) {
                        return
                    } else {
                        let selectedItem = document.querySelector('.selected');
                        selectedItem.classList.remove('selected');
                        let index = selectItems.indexOf(select);
                        select.classList.add('selected');

                        items[slideItem.current].classList.remove('active');
                        slideItem.current = index;

                        items[slideItem.current].classList.add('active');

                        let elementoLink = items[slideItem.current].querySelector('a')

                        let video = document.querySelector('video')

                        video.src = elementoLink.href                        

                        items[slideItem.current].scrollIntoView({
                            inline: "center",
                            behavior: "smooth"
                        })

                    }
                })
            })
        }
    }

</script>

<style>
    .slide-container {
        position: absolute;
        display: flex;
        flex-direction: column;
 
        bottom: 0;
        margin-bottom: 20px;
 
        width: 80%;
        height: 160px;
    }

    .slide-container a {
        pointer-events: none;
    }

    .slide-container::-webkit-scrollbar {
        display: none;
    }

    .slide-container {
        -ms-overflow-style: none;  /* IE and Edge */
        scrollbar-width: none;  /* Firefox */
    }

    .slide-content {
        width: 80%;
        height: 100%;
        border-radius: 8px;
        overflow: hidden;
        margin: 0 auto;
    }

    .slide-list {
        list-style: none;
        width: max-content;
        max-width: max-content;
    }
    
    .slide-item {
        display: inline-block;
        margin: 0px 40px;    
        opacity: 0.5;
    }
    
    .slide-item img {
        height: 140px;
    }

    .arrow-previous {
        display: flex;

        width: 24px;
        height: 24px;

        background-color: #075e81;
        border-radius: 8px;

        margin-right: 20px;
    }
    
    .arrow-previous:hover {
        background-color: #6AD3FC;
        transition: 0.7s;
    }

    .arrow-next {
        display: flex;
        order: 1;

        width: 24px;
        height: 24px;

        background-color: #075e81;
        border-radius: 8px;

        margin-left: 20px;
    }

    .arrow-next:hover {
        background-color: #6AD3FC;
        transition: 0.7s;
    }

    .active {
        opacity: 1;
    }
     
    /* select box */
    .select-container {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        
        width: max-content;
        
        margin: 0 auto;
        align-items: center;
    }
  
    .select-item {
        width: 12px;
        height: 12px;
        border-radius: 50%;
        background-color: #2F6C84;
        opacity: 0.5;
    }

    .selected {
        width: 12px;
        height: 12px;
        border-radius: 50%;
        background-color: #6AD3FC;
        opacity: 1;
    }


    /* Media queries */

    @media (max-width: 320px) {
        .slide-item img {
            height: 80px;
        }

        .slide-container {
            height: auto;
        }
    }

    @media (max-width: 420px) {
        .slide-container {
            bottom: 10%;
            width: 100%;
        }

        .slide-content {
            width: 100%;
        }

        .slide-item {
            margin: 0px 8px;
        }
    }


</style>