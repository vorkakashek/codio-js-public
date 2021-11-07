<template lang="pug">
.custom-cursor
	#cursor-big.custom-cursor__ball.custom-cursor__ball--big
	#cursor-small.custom-cursor__ball.custom-cursor__ball--small
</template>

<script>
import gsap from "gsap";

export default {
	props: {
		hoverClass: {
			type: String,
			default: "cursor-hover",
		},
	},

	mounted() {
		const cursorBig = document.getElementById("cursor-big"),
			cursorSmall = document.getElementById("cursor-small");

		// Event Listeners
		document.addEventListener("mousemove", onMouseMove);
		document.addEventListener("mousedown", onMouseHover);

		document.addEventListener("mouseover", e => {
			const target = e.target,
				parentLink = target.closest('a'),
				parentHoverClass = target.closest('.cursor-hover');
			if (target.tagName == 'A' || target.classList.contains(this.hoverClass) || parentLink !== null || parentHoverClass !== null) {
				onMouseHover();
			}
		});


		document.addEventListener('mouseover', e => {
			const target = e.target,
				parentLink = target.closest('a'),
				parentHoverClass = target.closest('.cursor-hover');
			
			if (target.tagName !== 'A' && !target.classList.contains(this.hoverClass) && parentLink == null && parentHoverClass == null) {
				onMouseHoverOut();
			}

			if (target.classList.contains('hire')) {
				gsap.to(cursorBig, 0.1, {
					scale: 3,
					opacity: 0,
					ease: "power1.inOut",
				});

				gsap.to(cursorSmall, 0.3, {
					scale: 10,
					opacity: 0,
					mixBlendMode: "difference",
					ease: "power1.inOut",
				});
				}
		});


		document.addEventListener("mouseup", onMouseHoverOut);
		document.addEventListener("mouseenter", () => {
			cursorBig.style.opacity = 1;
			cursorSmall.style.opacity = 1;
		});
		document.addEventListener("mouseleave", () => {
			cursorBig.style.opacity = 0;
			cursorSmall.style.opacity = 0;
		});
		

		// Event Handlers
		function onMouseMove(e) {
			gsap.to(cursorBig, 0.15, {
				ease: "easeInOut",
				x: e.clientX - 30,
				y: e.clientY - 30,
			});
			gsap.to(cursorSmall, 0, {
				x: e.clientX - 4,
				y: e.clientY - 4,
			});
		}
		function onMouseHover() {
			// console.log('onMouseHover')
			gsap.to(cursorBig, 0.1, {
				scale: 3,
				opacity: 0,
				ease: "power1.inOut",
			});

			gsap.to(cursorSmall, 0.3, {
				scale: 10,
				opacity: 1,
				mixBlendMode: "difference",
				ease: "power1.inOut",
			});
		}
		function onMouseHoverOut() {
			// console.log('onMouseHoverOut')
			gsap.to(cursorBig, 0.1, {
				scale: 1,
				backgroundColor: "unset",
				opacity: 1,
			});

			gsap.to(cursorSmall, 0.3, {
				scale: 1,
				opacity: 1,
				mixBlendMode: "unset",
			});
		}
	},
};
</script>


<style lang="scss" scoped>

@media screen and (min-width: 1199px) {

	.custom-cursor__ball {
		position: fixed;
		top: 0;
		left: 0;
		z-index: 99999;
		opacity: 0;
		pointer-events: none;
		transition: opacity 0.5s ease;
	}

	.custom-cursor__ball--big {
		content: "";
		width: 60px;
		height: 60px;
		border: 1px solid #fff;
		border-radius: 50%;
	}

	.custom-cursor__ball--small {
		content: "";
		width: 6px;
		height: 6px;
		background: #fff;
		border-radius: 50%;
	}
}
</style>