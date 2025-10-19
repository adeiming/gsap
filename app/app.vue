<script setup>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollSmoother } from "gsap/ScrollSmoother";

const loader = ref(true)
let smooth = null

useHead({
    title: 'GSAP',
})
onMounted(async () => {
    gsap.registerPlugin(ScrollTrigger, ScrollSmoother);
    await nextTick()

    smooth = ScrollSmoother.create({
        wrapper: "#smooth-wrapper",
        content: "#smooth-content",
        smooth: 2,
        smoothTouch: 0.1,
        effects: true
    })

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
            start: "top center",
            end: "bottom center",
            scrub: 1,
        }
    })
        .from('.__profil', {
            xPercent: 200,
            rotate: 5,
        })
        .from('._b2', {
            y: 100,
            opacity: 0,
        })
        .to('._b2', {
            y: 0,
        })
        .to('._b2', {
            y: 0,
        })
        .to('.__profil', {
            xPercent: -200,
            rotate: -5,
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
            end: "center center",
            scrub: 1,
        }
    })
    .from('.__kontak', {
        rotate: -5,
        xPercent: -100,
    })
    .from(`._b3`, {
        yPercent: 100,
        opacity: 0
    })
    .to('._botol', {
        left: '50%',
        xPercent: -50,
        rotate: 0,
        filter: 'saturate(200%)',
        scale: .8,
        onComplete: () => botol.play(),
        onReverseComplete: () => botol.pause(),
    })

});

const navigate = (e) => {
    e.preventDefault()
    smooth.scrollTo(e.target.hash, true, 'top top');
}
</script>

<template>
    <div class="backdrop-blur-lg fixed inset-0 z-20 bg-white/10" v-if="loader"></div>
    <img src="/botol.png" class="_botol size-60 fixed invisible z-0 saturate-100" />
    <div class="bg-amber-50 min-h-screen" id="smooth-wrapper">
        <header class="bg-amber-400/70 backdrop-blur flex gap-2 font-semibold text-amber-900 py-2 shadow-lg justify-between p-0 sm:px-10 top-0 z-10 sticky">
            <a href="#" class="p-2 _logo">AZIMA</a>
            <nav class="flex">
                <a href="#tentang" @click="navigate" class="_link p-2">Tentang</a>
                <a href="#profil" @click="navigate" class="_link p-2">Profil</a>
                <a href="#kontak" @click="navigate" class="_link p-2">Kontak</a>
            </nav>
        </header>
        <div class="overflow-hidden" id="smooth-content">
            <UContainer class="pb-25">
                <main class="text-lg text-black">
                    <section class="min-h-screen gap-2 flex justify-center items-center flex-col bg-amber-50 text-shadow-lg" id="_a">
                        <h1 class="_a font-semibold text-7xl sm:text-9xl text-center text-amber-600">
                            Makan Malam
                        </h1>
                        <h2 class="_a font-semibold text-6xl sm:text-8xl text-center text-amber-500">
                            Bersama Mantan
                        </h2>
                        <img src="/baso.png" class="_a size-60" />
                    </section>
                    <section class="bg-white rounded-xl relative overflow-hidden p-10 __botol" id="tentang">
                        <div class="sticky top-1 flex z-2">
                            <h1 class="text-xl font-semibold block bg-amber-600/20 backdrop-blur-lg text-amber-800 p-4">Tentang</h1>
                        </div>
                        <div class="text-center _b1">
                            <div class="space-y-5 py-10 md:py-30">
                                <p class="font-semibold text-xl">
                                    “Kisah di Balik Meja Ini”
                                </p>

                                <div>
                                    Malam, lampu redup, dan denting sendok di gelas —
                                    begitulah semua ini dimulai.
                                </div>

                                <div>
                                    Kami percaya, makanan punya cara sendiri untuk bercerita.
                                    Bahwa setiap suapan bisa membawa kita ke masa lalu,
                                    ke tawa yang dulu sederhana, ke momen yang dulu terasa utuh.
                                </div>

                                <div>
                                    “Makan Malam Bersama Mantan” lahir dari ide sederhana:
                                    bagaimana jika kenangan pahit dan manis bisa disatukan di atas meja yang sama,
                                    bukan untuk membuka luka, tapi untuk menutupnya dengan senyum.
                                </div>
                            </div>
                        </div>
                    </section>
                    <section class="bg-amber-100 rounded-xl relative overflow-hidden p-10 __profil" id="profil">
                        <div class="sticky top-1 flex z-2">
                            <h1 class="text-xl font-semibold block bg-amber-600/20 backdrop-blur-lg text-amber-800 p-4">Profil</h1>
                        </div>
                        <div class="text-center z-1 _b2">
                            <div class="space-y-5 py-10 md:py-30">
                                <p class="font-semibold text-xl">
                                    “Siapa di Balik Kisah Ini”
                                </p>

                                <p>
                                    Kami adalah orang-orang yang percaya bahwa perpisahan bukan akhir,
                                    dan bahwa kenangan bisa jadi sesuatu yang indah bila disajikan dengan hangat.
                                </p>

                                <p>
                                    Di balik meja dan lilin, ada tim kecil yang mencintai suasana,
                                    menghargai kenangan, dan memahami arti keheningan di antara dua orang yang pernah saling mencinta.
                                </p>

                                <p>
                                    Kami bukan sekadar penyaji makanan,
                                    kami perangkai suasana, pengantar rasa, dan pencipta momen yang tidak bisa dipesan ulang.
                                </p>

                            </div>
                        </div>
                    </section>
                    <section class="bg-white rounded-xl relative overflow-hidden p-10 __kontak" id="kontak">
                        <div class="sticky top-1 flex z-2">
                            <h1 class="text-xl font-semibold block bg-amber-600/20 backdrop-blur-lg text-amber-800 p-4">Kontak</h1>
                        </div>
                        <div class="text-center z-1 _b3">
                            <div class="space-y-5 py-10 md:py-30">
                                <p class="font-semibold text-xl">
                                    “Ingin Mengulang Cerita?”
                                </p>

                                <p>
                                    Mungkin malam ini bukan untuk kembali,
                                    tapi untuk berdamai dengan masa lalu.
                                </p>

                                <p>
                                    Jika kamu ingin memesan meja, mengirim pesan, atau sekadar berbagi cerita —
                                    kami selalu siap mendengarkan, dengan secangkir teh hangat dan lampu temaram yang menenangkan.
                                </p>

                                <p>
                                    Hubungi kami, bukan untuk mengulang yang telah berlalu,
                                    tapi untuk mengingat bahwa kenangan pun bisa disajikan dengan indah.
                                </p>
                            </div>
                        </div>
                    </section>
                    <section class="px-10 pt-30 pb-5 z-50 relative text-center font-bold">
                        &nbsp; 2025 AZIMA CORP
                    </section>
                </main>
            </UContainer>
        </div>
    </div>
</template>
