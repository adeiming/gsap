<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { Flip } from "gsap/Flip";

const loader = ref(true)
useHead({
    title: 'GSAP',
})
onMounted(async () => {
    gsap.registerPlugin(ScrollTrigger, Flip);
    await nextTick()
    loader.value = false

    gsap.timeline()
        .from("._logo", {
            opacity: 0,
            x: -50,
            duration: 0.5,
        })
        .from(
            "._link",
            {
                y: -20,
                opacity: 0,
                stagger: 0.1,
            },
            "<0.1"
        )
        .from("._a", {
            y: -20,
            opacity: 0,
            stagger: 0.2,
        })
        .fromTo("._botol", { opacity: 0, visibility: 'hidden', zIndex: -1 }, {
            opacity: 1,
            zIndex: 1,
            visibility: 'visible',
        })

    gsap.timeline({
        scrollTrigger: {
            trigger: "#_a",
            start: "center center",
            end: "bottom center",
            scrub: 1,
        },
    })
        .to("._a", {
            y: -20,
            scale: 1.5,
            stagger: 0.1,
        })

    gsap.timeline({
        scrollTrigger: {
            trigger: '.__botol',
            start: "top center",
            end: "bottom center",
            scrub: 1,
        }
    })
        .from('.__botol', {
            xPercent: -100,
            rotate: -5,
        })
        .from('._b1', {
            y: 100,
            opacity: 0
        }, '<0.5')
        .fromTo("._botol", {
            top: '55%',
            left: '100%',
            xPercent: -30,
            rotate: -10
        }, {
            left: '100%',
            xPercent: -90,
            opacity: 1,
            rotate: 0
        }, '<')
        .to("._botol", {
            rotate: 10,
        })
        .to("._botol", {
            rotate: 0
        })
        .to("._botol", {
            rotate: -10
        })
        .to("._b1", {
            y: -100,
            opacity: 0
        })
        .to('.__botol', {
            xPercent: 100,
            rotate: 5,
        })
        .to("._botol", {
            left: '100%',
            xPercent: -50
        }, '<0.5')

    gsap.timeline({
        scrollTrigger: {
            trigger: '.__profil',
            start: "top bottom",
            end: "bottom center",
            scrub: 1,
        }
    })
        .from('.__profil', {
            xPercent: 200,
            rotate: 5,
        })
        .from('._b2', {
            y: -100,
            opacity: 0
        })
        .to('._b2', {
            y: 100,
            opacity: 0
        })
        .to('.__profil', {
            xPercent: -200,
            rotate: -5
        })

    const botol = gsap.timeline({
        paused: true,
    }).fromTo('._botol', {top: '55%'},  {
        top: '60%',
        yoyo: true,
        duration: 3,
        repeat: -1,
        ease: 'none'
    })

    gsap.timeline({
        scrollTrigger: {
            trigger: '.__kontak',
            start: "top center",
            end: "20% center",
            scrub: 1,
        }
    })
    .from('.__kontak', {
        rotate: -5,
        xPercent: -100,
    })
    .from(`._b3`, {
        yPercent: -10,
        opacity: 0
    })
    .to('._botol', {
        left: '50%',
        xPercent: -50,
        rotate: 0,
        filter: 'saturate(200%)',
        onComplete: () => botol.play(),
        onReverseComplete: () => botol.pause(),
    })
});
</script>

<template>
    <div class="backdrop-blur-lg fixed inset-0 z-20 bg-white/10" v-if="loader"></div>
    <img src="/botol.png" class="_botol size-60 fixed invisible z-0 saturate-100" />
    <div class="bg-amber-50 min-h-screen">
        <header class="bg-amber-400/70 backdrop-blur flex gap-2 font-semibold text-amber-900 py-2 shadow-lg justify-between p-0 sm:px-10 top-0 z-10 sticky">
            <div class="p-2 _logo">SOHO</div>
            <nav class="flex">
                <a href="#" class="_link p-2">Tentang</a>
                <a href="#" class="_link p-2">Profil</a>
                <a href="#" class="_link p-2">Kontak</a>
            </nav>
        </header>
        <UContainer class="overflow-hidden">
            <main class="text-lg pb-10 text-black">
                <section class="min-h-screen gap-2 flex justify-center items-center flex-col bg-amber-50 text-shadow-lg" id="_a">
                    <h1 class="_a font-semibold text-7xl sm:text-9xl text-center text-amber-600">
                        Makan Malam
                    </h1>
                    <h2 class="_a font-semibold text-6xl sm:text-8xl text-center text-amber-500">
                        Bersama Mantan
                    </h2>
                    <img src="/baso.png" class="_a size-60" />
                </section>
                <section class="min-h-screen bg-white rounded-xl relative overflow-hidden p-10 __botol">
                    <div class="sticky top-18 flex z-2">
                        <h1 class="text-xl font-semibold block bg-amber-600 text-white p-4">Tentang</h1>
                    </div>
                    <div class="absolute inset-0 flex justify-center items-center p-10 text-center _b1">
                        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Laboriosam eius quas laborum,
                        repudiandae incidunt consequatur est repellendus dolore? Repudiandae necessitatibus amet
                        reiciendis eaque, accusamus nostrum commodi nihil assumenda consectetur? Tempore!
                    </div>
                </section>
                <section class="min-h-screen bg-amber-100 rounded-xl relative overflow-hidden p-10 __profil">
                    <div class="sticky top-18 flex z-2">
                        <h1 class="text-xl font-semibold block bg-amber-600 text-white p-4">Profil</h1>
                    </div>
                    <div class="absolute inset-0 flex justify-center items-center p-10 text-center z-1 _b2">
                        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Laboriosam eius quas laborum,
                        repudiandae incidunt consequatur est repellendus dolore? Repudiandae necessitatibus amet
                        reiciendis eaque, accusamus nostrum commodi nihil assumenda consectetur? Tempore!
                    </div>
                </section>
                <section class="min-h-screen bg-white rounded-xl relative overflow-hidden p-10 mb-10 __kontak">
                    <div class="sticky top-18 flex z-2">
                        <h1 class="text-xl font-semibold block bg-amber-600 text-white p-4">Kontak</h1>
                    </div>
                    <div class="absolute inset-0 flex justify-center items-center p-10 z-10 text-center _b3">
                        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Laboriosam eius quas laborum,
                        repudiandae incidunt consequatur est repellendus dolore? Repudiandae necessitatibus amet
                        reiciendis eaque, accusamus nostrum commodi nihil assumenda consectetur? Tempore!
                    </div>
                </section>
            </main>
        </UContainer>
    </div>
</template>
