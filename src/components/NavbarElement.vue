<template>
    <section class="w-full">
		<div class="w-full" style="height: 81px;">
			<!-- Navbar start -->
				<nav class="w-screen fixed bg-opacity-90 bg-black p-4 lg:px-20 flex justify-between z-50">
				<!-- Logo start -->
				<div class="h-full flex flex-col justify-center cursor-pointer" @click="openLinkServer">
					<p class="tracking-widest font-semibold text-white">Farmer 🧑🌾</p>
					<p class="tracking-widest font-light text-white">Việt Nam</p>
				</div>
				<!-- Logo end -->

				<!-- Toggler start -->
				<button role="menubar" class="md:hidden" @click="navToggle()">
					<i class="fa-solid fa-bars text-2xl"></i>
				</button>
				<!-- Toggler end -->

				<!-- Menu content start -->
				<div class="absolute left-0 right-0 translate-y-16 bg-opacity-90 bg-black md:bg-none md:bg-opacity-0 shadow hidden md:flex flex-col gap-4 items-center p-4 md:flex-row md:static md:shadow-none md:translate-y-0" role="menu" aria-expanded="false">
					<!-- Links start -->
					<a href="#" role="menuitem">
						<p class="mx-4 text-white">Home</p>
					</a>

					<a href="#" role="menuitem">
						<p class="mx-4 text-white">About</p>
					</a>

					<a href="#" role="menuitem">
						<p class="mx-4 text-white">Explore</p>
					</a>
<!-- 
					<button class="btn" role="menuitem">
						Contact us
					</button> -->
					<!-- Links end -->
				</div>
				<!-- Menu content end -->
			</nav>
			<!-- Navbar end -->
		</div>
	</section>
</template>

<script>

export default {
    methods: {
		// Toogle navbar mode 
        navToggle() {
			let menu = document.querySelector("[role='menu']");
			let isExpanded = menu.getAttribute('aria-expanded');
			menu.setAttribute('aria-expanded', !isExpanded);
			menu.classList.toggle('hidden');
			menu.classList.toggle('flex');
		},
		openLinkServer: function(){
			window.open("https://discord.gg/farmer-vn", "_blank")
		}
    }
}
</script>

<style>

</style>