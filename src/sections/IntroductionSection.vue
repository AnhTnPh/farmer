<template>
  <section id="introduction-section" class="py-12">
    <div class="w-full flex flex-col h-full md:justify-center module-video" style="align-items: center">
        <video class="w-full h-full video-cover" playsinline loop autoplay muted preload="true">
            <source :src='require("@/assets/video/introduction_home.mp4")' type="video/mp4">
        </video>
        <div class="invite-server">
          <div class="w-full flex flex-col text-center" style="display: block;position: relative;">
            <span class="text-white font-bold font-semibold">Chào mừng bạn đến với cộng đồng</span>
          </div>
          <div class="w-full flex flex-col">
            <span class="text-9xl text-white tracking-widest font-semibold title-server">Farmer</span>
          </div>
          <div class="w-full md:w-1/2 flex flex-col m-auto mt-2">
            <button class="btn btn-join" role="menuitem" @click="inviteDiscordLink">
              Tham gia ngay
            </button>
          </div>
        </div>
    </div>
  </section>
</template>

<script>
export default {
  methods: {
    inviteDiscordLink(){
      window.open("https://discord.gg/farmer-vn", "_blank")
    }
  }
}
</script>

<style lang="scss" scoped>
$yellow: #f1c40f;
.btn-join {
  border: 1px solid white;
  transition: 1s ease-in-out;
  background: transparent;
  background: {
    image: linear-gradient(45deg,$yellow 50%, transparent 50%);
    position: 100%;
    size: 400%;
  }
  transition: background 800ms ease-in-out;
  
  &:hover {
    background-position: 0;
  }
}
.video-cover {
  object-fit: cover;
  // border-radius: 0 0 0 50px;
}
.module-video {
  border-radius: 0 0 0 60px;
  height: 40rem;
}
.invite-server {
  margin: 3.5rem 0;
  text-align: center;
  position: absolute;
  top: 15rem;
  @media screen and (max-width: 500px) {
    .title-server {
      font-size: 5rem;
    }
  }
}
</style>