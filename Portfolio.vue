<template lang="pug">


h1 Cases

.grid-template
	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed="-.1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/1.png')" data-speed=".05")
			h2 Tarologist LyalyaMua
			.parallax-block-tag Landing Page

	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed=".1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/2.png')" data-speed=".05")
			h2 Vera Coffee & Tea
			.parallax-block-tag e-Shop

	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed="-.1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/4.png')" data-speed=".05")
			h2 Clinic of Dr. Vorobjev
			.parallax-block-tag Corporative website

	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed=".1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/3.png')" data-speed=".05")
			h2 Conscious eating
			.parallax-block-tag Online learning service

	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed="-.1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/1.png')" data-speed=".05")
			h2 Alex GCB
			.parallax-block-tag Landing Page

	a.parallax-block.parallax-trigger.parallax-scroll-trigger(href="#" target="_blank" data-speed=".1")
		.parallax-block-image
			figure
				img(:src="require('@/assets/portfolio/1.png')" data-speed=".05")
			h2 MYTATTOO.PRO
			.parallax-block-tag Online service

</template>

<script>
import gsap from 'gsap'
import {ScrollTrigger} from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

export default {
	mounted() {

		ScrollTrigger.matchMedia({
			"(min-width: 1200px)": function() {
				gsap.timeline({
					scrollTrigger: {	
						trigger: "#app",
						start: "top top",
						end: "bottom bottom",
						scrub: true,
					}
				})
				.to('h1', {
					y: 300,
					ease: 'easeOut'
				})
				.to(".parallax-scroll-trigger", {
					y: (i, target) => -ScrollTrigger.maxScroll(window) * target.dataset.speed,
				})
			}
		});

		document.addEventListener('mousemove', e => {
			const target = e.target

			if (target.classList.contains('parallax-trigger') || target.closest('.parallax-trigger')) {
				const cx = Math.ceil(window.innerWidth / 2),
					cy = Math.ceil(window.innerHeight / 2),
					dx = e.clientX - cx,
					dy = e.clientY - cy,
					tiltx = (dy / cy),
					tilty = - (dx / cx),
					radius = Math.sqrt(Math.pow(tiltx, 2) + Math.pow(tilty, 2)),
					degree = (radius * 20);

				gsap.to(target.querySelector('.parallax-block-image'), {
					transform: 'rotate3d(' + tiltx / 1 + ', ' + tilty / 1 + ', 0, ' + degree / 3 + 'deg)',
				});

				gsap.to(target.querySelector('img'), {
					x: tilty * 50,
					y: tiltx,
				}) 
			}
		});

		document.addEventListener('mouseout', e => {
			const target = e.target;

			if (target.matches('.parallax-block')) {
				gsap.to(target.querySelector('.parallax-block-image'), {
					ease: "power1.inOut",
					transform:'rotate3d(' + 0 + ', ' + 0 + ', 0, ' + 0 + 'deg)',
				})

				gsap.to(target.querySelector('img'), {
					ease: "power1.inOut",
					x: 0,
					y: 0,
				}) 
			}
		});
	},
	methods: {
		// scrollAnimation() {
		// 	gsap.timeline({
		// 		scrollTrigger: {	
		// 			trigger: "#app",
		// 			start: "top top",
		// 			end: "bottom bottom",
		// 			scrub: true,
		// 		}
		// 	})
		// 	.to('h1', {
		// 		y: 300,
		// 		ease: 'easeOut'
		// 	})
		// 	.to(".parallax-scroll-trigger", {
		// 		y: (i, target) => -ScrollTrigger.maxScroll(window) * target.dataset.speed,
		// 	})
		// }
	},
}
</script>


<style lang="scss" scoped>

h1 {
	text-align: left;
	font-size: calc(10rem + 1vw);
	// font-weight: 100;
	// text-transform: uppercase;
	letter-spacing: 1rem;
	font-family: 'NeueMetana', sans-serif;
	font-weight: 700;
	max-width: 100%;
	@include respond-to(large) {
		font-size: calc(10vw);
		max-width: 100%;
	}
}

.grid-template {
	// display: flex;
	// align-items: flex-start;
	// flex-wrap: wrap;

	display: grid;
    grid-template-columns: repeat(2, 1fr);
    // grid-gap: 40px;
    gap: 100px;
    align-content: flex-start;

	overflow: hidden;
	margin-top: 100px;
	margin-bottom: 100px;

	@media screen and (max-width: 1440px) {
		display: block;
	}
}

.parallax-block {
	// width: 50%;
	// padding: 50px;
	// padding: 20px;
	box-sizing: border-box;
	display: block;
	img {
		max-width: 100%;
	}

	@include respond-to(xxlarge) {
		margin-bottom: 100px;
	}

	@include respond-to(xxlarge-plus) {
		&:nth-child(even) {
			// margin-top: 50%;
			margin-top: 30%;

			h2 {
				left: 20px;
				right: unset;
			}

			.parallax-block-image {
				display: flex;
				justify-content: flex-end;
			}

			.parallax-block-tag {
				left: 20px;
				right: unset;
			}
		}
	}
	

	&:hover {
		h2 {
			text-decoration: underline;
			// background-color: rgba(0,0,0,.25);
			backdrop-filter: brightness(0.85) blur(5px);
		}
		.parallax-block-tag {
			// backdrop-filter: brightness(0.85) blur(5px);
		}
	}

}

.parallax-trigger {
	transform: perspective(2000px);
	transform-style: preserve-3d;
	perspective: 2000px;
	* {
		user-select: none !important;
		pointer-events: none !important;
	}	
}

.parallax-block-image {
	transform-style: preserve-3d;
	transform: translateZ(0px);
	position: relative;
	// padding: 20px;
	display: flex;
	text-decoration: none;
	color: #fff;

	h2 {
		position: absolute;
		right: 20px;
		bottom: 20px;
		transform: translateZ(120px);
		font-size: 56px;
		padding: 20px 40px;
		transition: all .3s ease;
		backdrop-filter: brightness(1) blur(0px);
	}

	.parallax-block-tag {
		position: absolute;
		transform: translateZ(120px);
		bottom: 10px;
		right: 20px;
		text-transform: uppercase;
		letter-spacing: .5rem;
		padding: 20px 40px;
	}

	@include respond-to (large) {
		figure {
			max-width: 100%;
		}
		.parallax-block-tag {
			width: 100%;
			right: 0;
			text-align: center;
		}
	}
}


figure {
	overflow: hidden;
	max-width: 90%;
	height: 580px;
	display: flex;
	justify-content: center;
	align-items: center;
	margin: 0;
	img {
		width: 120%;
		height: 120%;
		object-fit: cover;
		object-position: center;
		max-width: unset !important;
	}
}

@media screen and (max-width: 1440px) {
	.parallax-block {
		width: 100%;
	}
}

</style>