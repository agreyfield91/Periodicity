<template>
	<div class="element" :style="renderStyle(trendToDisplay, element)">
		<div class="value">{{renderValue(trendToDisplay, element) || 'unknown'}}
		</div>
		<div class="symbol">{{element.symbol}}</div>
		<!-- <div class="name">{{element.name}}</div> -->
	</div>
</template>

<script>
export default {
	name: 'TrendCard',
	props: ['element', 'trendToDisplay'],
	data() {
		return {};
	},
	methods: {
		convertMass(element) {
			var n = element.atomicNumber;
			var m = element.atomicMass;
			var exceptions = [57, 58, 59, 60, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 90, 91, 92];
			if ((n <= 83 && n !== 61 && n !== 43) || exceptions.indexOf(n) > -1) {
				m = m.slice(0, -3);
				return parseFloat(parseFloat(m).toFixed(3));
			} else {
				return m.toString();
			}
		},
		renderValue(trend, element) {
			//target for refractor
			if (trend === 'Ionization Energy') {
				return element.ionizationEnergy;
			} else if (trend === 'Electronegativity') {
				return element.electronegativity;
			} else if (trend === 'Atomic Radius') {
				return element.atomicRadius;
			} else if (trend === 'Electron Affinity') {
				return element.electronAffinity;
			} else if (trend === 'Melting Point') {
				return element.meltingPoint;
			} else if (trend === 'Density') {
				return element.density;
			}
		},
		renderStyle(trend, element) {
			//target for refractor
			if (trend === 'Ionization Energy') {
				var opacity = element.ionizationEnergy / 2372;
				var background = `rgba(195, 37, 60, ${opacity}`;
			} else if (trend === 'Electronegativity') {
				var opacity = element.electronegativity / 3.98;
				var background = `rgba(239, 187, 49, ${opacity}`;
			} else if (trend === 'Atomic Radius') {
				var opacity = element.atomicRadius / 225;
				var background = `rgba(90, 137, 219, ${opacity}`;
			} else if (trend === 'Electron Affinity') {
				var opacity = element.electronAffinity / -349;
				var background = `rgba(175, 26, 163, ${opacity}`;
			} else if (trend === 'Melting Point') {
				var opacity = element.meltingPoint / 3823;
				var background = `rgba(180, 85, 30, ${opacity}`;
			} else if (trend === 'Density') {
				var opacity = element.density / 22.65;
				var background = `rgba(106, 70, 140, ${opacity}`;
			}
			return `background: ${background}`;
		},
	},
};
</script>

<style lang="scss" scoped>
.element {
	color: rgba(245, 245, 245, 0.55);
	width: 100%;
	height: 100%;
	box-sizing: border-box;
	text-align: center;
	padding: 0.2vw;
	transition: 0.4s;
	transition-timing-function: ease;
	background: grey;
	.value {
		text-align: center;
		color: rgba(245, 245, 245, 0.5);
		font-size: 0.65vw;
		margin-top: 0.5vw;
		transition: 0.2s;
		transition-timing-function: ease;
	}
	.symbol {
		margin-top: -0.2vw;
		font-weight: 600;
		font-size: 2vw;
		opacity: 0.8;
	}
	&:hover {
		color: rgba(255, 255, 255, 0.95);
		.value {
			color: rgba(245, 245, 245, 0.8);
		}
	}
}
@media only screen and (max-width: 600px) {
	.element {
		color: rgba(245, 245, 245, 0.55);
		width: 100%;
		height: 100%;
		box-sizing: border-box;
		text-align: center;
		padding: 0.4vw;
		.value {
			text-align: center;
			color: rgba(245, 245, 245, 0.5);
			font-size: 1.2vw;
			margin-top: 1vw;
			transition: 0.2s;
			transition-timing-function: ease;
		}
		.symbol {
			margin-top: -0.4vw;
			font-weight: 600;
			font-size: 4vw;
			opacity: 0.8;
		}
	}
}
</style>
