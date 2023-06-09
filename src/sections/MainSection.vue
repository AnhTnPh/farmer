<template>
    <!-- Main section start -->
	<section :class="{'px-12 lg:px-32 py-16':!isMobile, 'w-full flex flex-col mt-4 lg:px-4 px-4' : isMobile }">
		<div class="w-full flex">
			<span :class="{'text-7xl font-bold': !isMobile, 'text-3xl font-bold' : isMobile}" style="color: #ff4655;">Nổi bật</span>
		</div>
		<div :class="{'w-full flex':!isMobile, 'w-full':isMobile}">
			<div class="w-full md:w-1/2 h-full flex flex-col md:justify-center ">
				<!-- Main text start -->
				<h1 :class="{'uppercase text-5xl xl:text-5xl mb-4 font-semibold':!isMobile, 'uppercase text-3xl xl:text-3xl mb-4 font-semibold':isMobile} ">
					Cùng đăng tải highlight bản thân !!!
				</h1>
				<p class="capitalize xl:w-1/2 text-stone-500">
					Là nơi thỏa sức vui chơi và đăng tải những video nổi bật của mình. Bạn hãy đồng hành cùng Farmer, Farmer sẽ luôn đồng hành cùng bạn
				</p>
				<!-- Main text end -->

				<!-- Social links start -->
				<div class="flex mt-3 gap-8">
					<a href="#">
						<i class="fa-brands fa-instagram socialIcon"></i>
					</a>
					<a href="#">
						<i class="fa-brands fa-linkedin socialIcon"></i>
					</a>
					<a href="#">
						<i class="fa-brands fa-facebook socialIcon"></i>
					</a>
					<a href="#">
						<i class="fa-brands fa-dribbble socialIcon"></i>
					</a>
					<a href="#">
						<i class="fa-brands fa-pinterest socialIcon"></i>
					</a>
				</div>
				<!-- Social links end -->
			</div>

			<!-- Photographer image start -->
			<div :class="{'h-full w-full md:w-1/2 flex flex-col':!isMobile, 'h-full w-full mt-4':isMobile}" style="align-items: end;">
				<video class="w-full h-full video-cover" playsinline loop autoplay muted preload="true">
					<source :src='require("@/assets/video/Chienscon.mp4")' type="video/mp4">
				</video>
			</div>

			<!-- Photographer image end -->
		</div>

		<!-- "More" button start -->
		<div class="w-full h-20 flex justify-start md:justify-center items-center">
			<a href="#about-section">
				<i class="fa-solid fa-arrow-down transition text-stone-100 text-xl bg-stone-700 rounded-full shadow p-4 hover:-translate-y-2 hover:shadow-xl"></i>
			</a>
		</div>
		<!-- "More" button end -->

	</section>
	<!-- Main section end -->
</template>

<script>
export default {
	data(){
		return {
			isMobile: false
		}
	},
	methods:{
		checkDevice() {
			if( /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent) ) this.isMobile = true;
			else this.isMobile = false;
		}
	},
	mounted() {
		this.checkDevice();
	}
}
</script>

<style>

</style>