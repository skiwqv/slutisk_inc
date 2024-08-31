<template>
  <div>
    <div ref="bgImage" class="container" id="zoom-out">
      <h2>JUNGLE</h2>
      <img class="bg-img" src="../assets/images/jungle.png" alt="" />
    </div>
    <div ref="horizontal" class="horizontal-scroll-container">
      <div class="horizontal-content" ref="scrollText">
        <h2>Welcome to the Jungle</h2>
      </div>
    </div>
    <div class="container" id="zoom-in">
      <h2>Snake</h2>
      <div ref="animalWrapper" class="animal-wrapper">
        <img class="animal-image" src="../assets/images/snake.png" alt="" />
        <p class="animal-description">
          The python is one of the largest snake species in the world. It is a
          non-venomous constrictor found in the tropics of Africa and Asia.
        </p>
      </div>
    </div>
    <div ref="horizontalLion" class="lion-horizontal">
      <section class="panel red">
        <h2>Lion</h2>
      </section>
      <section class="panel">
        <div class="animal-wrapper">
          <img class="animal-image" src="../assets/images/lion.png" alt="" />
          <p class="animal-description">
            Lions have strong, compact bodies and powerful forelegs, teeth and
            jaws for pulling down and killing prey.
          </p>
        </div>
      </section>
    </div>
    <div class="container video-container">
      <video
        class="video"
        ref="monkeyVideo"
        src="../assets/video/monkey.mp4"
        muted
        autoplay
        loop
      ></video>
      <h2 class="video-text">Monkey</h2>
    </div>
    <div class="container" id="giraffe-zoom-out">
      <SVGComponent class="girafe"></SVGComponent>
      <p class="animal-description">
        The tallest land mammal, with a neck as long as 6 feet, the giraffe is
        also well known for the unique brown and white pattern on its coat and
        its lengthy eyelashes and legs.
      </p>
    </div>
    <div class="container dark-green">
      <h2 class="outline">Jungle Forest</h2>
      <div class="jungle-images">
        <img src="../assets/images/jungle1.jpg" alt="" />
        <img src="../assets/images/jungle2.jpg" alt="" />
        <img src="../assets/images/jungle3.jpg" alt="" />
        <img src="../assets/images/jungle4.jpg" alt="" />
      </div>
    </div>
    <section class="comparisonSection">
      <div class="comparisonImage beforeImage">
        <img src="../assets/images/water.jpg" alt="before" />
      </div>

      <div class="comparisonImage afterImage">
        <img src="../assets/images/water1.jpg" alt="after" />
      </div>

      <div class="comparisonImage thirdImage">
        <img src="../assets/images/water2.jpg" alt="third" />
      </div>
    </section>
    <div class="container observe">
      <h2>Ready for more?</h2>
      <div class="carousel">
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal1.jpg"
            alt="Animal 1"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal2.jpg"
            alt="Animal 2"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal3.jpg"
            alt="Animal 3"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal4.jpg"
            alt="Animal 4"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal5.jpg"
            alt="Animal 5"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal6.jpg"
            alt="Animal 6"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal7.jpg"
            alt="Animal 7"
          />
        </div>
        <div class="carousel-image">
          <img
            class="animal-image marg"
            src="../assets/images/animal8.jpg"
            alt="Animal 8"
          />
        </div>
      </div>
    </div>
    <div class="container socials">
      <h2 class="socials-heading">Socials</h2>
      <div class="icon-wrapper">
        <Inst class="icon" @click="toInst"> </Inst>
        <LinkedIn class="icon" @click="toLinked"> </LinkedIn>
        <telegram class="icon" @click="toTelegram"> </telegram>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { Observer } from "gsap/Observer";
import SVGComponent from "@/components/giraffe.vue";
import Inst from "@/components/instagram.vue";
import telegram from "@/components/telegram.vue";
import LinkedIn from "@/components/linkedIn.vue";

gsap.registerPlugin(ScrollTrigger, Observer);

const bgImage = ref(null);
const horizontal = ref(null);
const scrollText = ref(null);
const animalWrapper = ref(null);
const horizontalLion = ref(null);
const monkeyVideo = ref(null);

const toInst = () => {
  window.open("https://www.instagram.com/skiwqv", "_blank");
};
const toLinked = () => {
  window.open("https://www.linkedin.com/in/andrey-koshelev0212/", "_blank");
};
const toTelegram = () => {
  window.open("https://t.me/skiwqv", "_blank");
};

const initAnimations = () => {
  const { innerHeight } = window;

  // Убедитесь, что элементы существуют
  // Анимация увеличения масштаба изображения
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: bgImage.value,
      pin: true,
      end: `+=${innerHeight * 1.3}`,
      scrub: 3,
    },
  });

  tl.fromTo(
    bgImage.value.querySelector("img"),
    {
      scale: 1,
      ease: "none",
    },
    {
      scale: 3,
      duration: 3,
    }
  );

  // Анимация горизонтального скролла текста
  const scrollWidth = scrollText.value.scrollWidth;
  const duration = 2; // Продолжительность анимации в секундах

  gsap.fromTo(
    scrollText.value,
    { xPercent: 130 },
    {
      xPercent: -100,
      duration: duration,
      ease: "none",
      scrollTrigger: {
        trigger: horizontal.value,
        start: "top top",
        end: `+=${scrollWidth}`, // Длина скролла
        scrub: 3,
        pin: true,
      },
    }
  );

  // Анимация появления заголовка
  const stl = gsap.timeline({
    scrollTrigger: {
      trigger: "#zoom-in",
      pin: true,
      end: `+=${innerHeight * 1.3}`,
      scrub: 3,
    },
  });
  stl.to("#zoom-in h2", {
    scale: 500,
    duration: 3,
  });

  // Анимация появления обертки с изображением
  stl.from(
    animalWrapper.value,
    {
      opacity: 0,
      duration: 3,
    },
    "<"
  );

  let horizontalSections = gsap.utils.toArray(".lion-horizontal");
  horizontalSections.forEach((container) => {
    let sections = container.querySelectorAll(".panel");

    gsap.to(sections, {
      xPercent: -100 * (sections.length - 1),
      ease: "none",
      scrollTrigger: {
        trigger: container,
        pin: true,
        scrub: 1,
        // base vertical scrolling on how wide the container is so it feels more natural.
        end: "+=3500",
      },
    });
  });
  const videoTimeline = gsap.timeline({
    scrollTrigger: {
      trigger: monkeyVideo.value,
      start: "top center",
      end: "bottom center",
      scrub: true,
    },
  });

  videoTimeline.fromTo(
    ".video-text",
    { opacity: 0, scale: 1 },
    { opacity: 1, scale: 1.5, duration: 3, ease: "power2.inOut" },
    "<"
  );
  const gtl = gsap.timeline({
    scrollTrigger: {
      trigger: "#giraffe-zoom-out",
      pin: true,
      end: `+=${innerHeight * 1.3}`,
      scrub: 3,
    },
  });
  gtl.fromTo(
    ".girafe",
    {
      y: 200,
      x: 700,
    },
    {
      y: 0,
      x: 0,
      rotate: 360,
      duration: 2,
    }
  );
  gtl.fromTo(
    "#giraffe-zoom-out p",
    { opacity: 0 },
    {
      opacity: 1,
      duration: 1,
    },
    "<"
  );
  const jungleImages = document.querySelectorAll(".jungle-images img");

  // Анимация разъезда картинок от текста Jungle Forest
  gsap
    .timeline({
      scrollTrigger: {
        trigger: ".dark-green",
        start: "top top",
        end: "bottom center",
        scrub: 2,
        pin: true,
      },
    })
    .to(jungleImages, {
      x: (i) => (i % 2 === 0 ? -50 : 50), // Разъезжаются в разные стороны
      y: (i) => (i % 2 === 0 ? -200 : 200), // Разъезжаются вверх и вниз
      scale: (i) => 0.8 + i * 0.2, // Разные размеры
      rotation: (i) => i * 10, // Поворот для эффекта
      stagger: 0.2,
      ease: "power2.out",
      duration: 2,
    });
  gsap.utils.toArray(".comparisonSection").forEach((section) => {
    let tl = gsap.timeline({
      scrollTrigger: {
        trigger: section,
        start: "center center",
        // makes the height of the scrolling (while pinning) match the width, thus the speed remains constant (vertical/horizontal)
        end: () => "+=" + section.offsetWidth,
        scrub: true,
        pin: true,
        anticipatePin: 1,
      },
      defaults: { ease: "none" },
    });
    // animate the container one way...
    tl.fromTo(
      section.querySelector(".afterImage"),
      { xPercent: 100, x: 0 },
      { xPercent: 0 }
    )
      // ...and the image the opposite way (at the same time)
      .fromTo(
        section.querySelector(".afterImage img"),
        { xPercent: -100, x: 0 },
        { xPercent: 0 },
        0
      )

      .fromTo(
        section.querySelector(".thirdImage"),
        { xPercent: 100, x: 0 },
        { xPercent: 0 },
        1
      )
      // ...and the image the opposite way (at the same time)
      .fromTo(
        section.querySelector(".thirdImage img"),
        { xPercent: -100, x: 0 },
        { xPercent: 0 },
        1
      );
  });
  const images = document.querySelectorAll(".carousel-image");
  const radius = 242;
  const progress = {
    value: 0,
  };
  const carousel = document.querySelector(".carousel");

  Observer.create({
    target: carousel,
    type: "wheel,pointer",
    onPress: (self) => {
      carousel.style.cursor = "grabbing";
    },
    onRelease: (self) => {
      carousel.style.cursor = "grab";
    },
    onChange: (self) => {
      gsap.killTweensOf(progress);
      const p =
        self.event.type === "wheel"
          ? self.deltaY * -0.0005
          : self.deltaX * 0.05;
      gsap.to(progress, {
        duration: 2,
        ease: "power4.out",
        value: `+=${p}`,
      });
    },
  });

  const animate = () => {
    images.forEach((image, index) => {
      const theta = index / images.length - progress.value;
      const x = -Math.sin(theta * Math.PI * 2) * radius;
      const y = Math.cos(theta * Math.PI * 2) * radius;
      image.style.transform = `translate3d(${x}px, 0px, ${y}px) rotateY(${360 * -theta}deg)`;
      const c = Math.floor((index / images.length) * 360);
      image.style.background = `hsla(${c}, 90%, 50%, .5)`;
    });
  };
  gsap.ticker.add(animate);

  gsap.from(".socials-heading", {
    y: -100, // Сверху вниз
    opacity: 0,
    duration: 1,
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".socials",
      start: "top 80%", // Анимация запускается, когда секция появляется на 80% экрана
    },
  });

  // Анимация для ссылок снизу вверх
  gsap.from(".icon", {
    y: 100, // Снизу вверх
    opacity: 0,
    duration: 1,
    stagger: 0.2, // Задержка между анимацией каждой иконки
    ease: "power2.out",
    scrollTrigger: {
      trigger: ".socials",
      start: "top 80%", // Анимация запускается, когда секция появляется на 80% экрана
    },
  });
};
onMounted(() => {
  initAnimations();
});
</script>

<style>
.container {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}
.observe {
  display: flex;
  flex-direction: column;
  background-color: #2c653b;
}
.horizontal-scroll-container {
  height: 100vh;
  position: relative;
  width: 3000px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  overflow: hidden;
  background-color: #2c653b;
}
.horizontal-content {
  display: flex;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
}

h2 {
  font-weight: 600;
  font-size: 120px;
  color: #fff;
  margin: 0;
}

.bg-img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
  top: 0;
  left: 0;
}
.animal-image {
  width: 250px;
  height: 250px;
}
.marg {
  width: 200px;
  height: 300px;
}
.girafe {
  height: 500px;
  width: 400px;
}
.animal-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 50px;
}
.animal-description {
  max-width: 400px;
  color: #fff;
  font-size: 48px;
}
.lion-horizontal {
  overscroll-behavior: none;
  width: 600%;
  height: 100vh;
  display: flex;
  flex-wrap: nowrap;
  background-color: #2c653b;
}
.panel {
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}
.video-container {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 80px;
}

.video {
  width: 80vw;
  height: auto;
  z-index: 1;
}

.video-text {
  position: absolute;
  color: #fff;
  font-size: 100px;
  font-weight: bold;
  z-index: 2;
}
.dark-green {
  background-color: rgb(25, 55, 18);
}
.outline {
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: white;
  position: relative;
  z-index: 100;
}
.jungle-images {
  display: flex;
  justify-content: space-around;
  width: 100%;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
}

.jungle-images img {
  width: 20vw;
  height: auto;
  opacity: 0.8;
}
.comparisonSection {
  position: relative;
  height: 100vh;
  background-color: #111;
  color: white;
  overflow-x: hidden;
}
.comparisonImage {
  width: 100%;
  height: 100%;
}

.thirdImage,
.afterImage {
  position: absolute;
  overflow: hidden;
  top: 0;
  transform: translate(100%, 0px);
}

.thirdImage img,
.afterImage img {
  transform: translate(-100%, 0px);
}

.comparisonImage img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
}
.carousel {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  transform: rotateX(-20deg) translateY(-70px);
  transform-style: preserve-3d;
  perspective: 800px;
  user-select: none;
  cursor: grab;
}

.carousel-image {
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -100px 0 0 -100px;
  width: 200px;
  height: 200px;
  transform: translate3d(0, 0, -10px);
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  transform-origin: 50% 50%;
}

.socials {
  display: flex;
  flex-direction: column;
}
.icon-wrapper {
  display: flex;
  gap: 30px;
}
.icon {
  fill: #fff;
  width: 70px;
  cursor: pointer;
  height: 70px;
  transition:
    transform 0.3s,
    fill 0.3s;
}
.icon:hover {
  transform: scale(1.1);
  fill: #e6e6e6;
}
@media (max-width: 600px) {
  .carousel {
    transform: rotateX(-10deg) scale(0.6) translateY(-60px);
  }
}

@media (max-width: 768px) {
  h2 {
    font-size: 80px;
  }
  .animal-description {
    font-size: 24px;
  }
}
</style>
