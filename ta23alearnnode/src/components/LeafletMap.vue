<script setup>
//import * as L from 'leaflet';
import L from "leaflet";
import "leaflet/dist/leaflet.css";
import "leaflet/dist/images/marker-icon-2x.png";
import "leaflet/dist/images/marker-icon.png";
import "leaflet/dist/images/marker-shadow.png";
import { onMounted, useId, watch } from "vue";

const { center, zoom } = defineProps(["center", "zoom"]);
const id = "map-" + useId();
let map;
onMounted(() => {
	map = L.map(id).setView(center, zoom);
	L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
		maxZoom: 19,
		attribution:
			'&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
	}).addTo(map);
	var marker = L.marker([59.4269, 24.7434]).addTo(map);
	var marker = L.marker([59.438511, 24.790931]).addTo(map);
	var polygon = L.polygon([
		[59.438690065086675, 24.790947325689241],
		[59.43866707980278, 24.791067223474258],
		[59.438715068286356, 24.791088265393288],
		[59.438679, 24.791309],
		[59.43827796911317, 24.7910285862434],
		[59.438314905473604, 24.790815191005905],
		[59.438354115024964, 24.790848048064333],
		[59.438374799682464, 24.790736225470305],
	]).addTo(map);
});
watch(
	() => center,
	(center, oldCenter) => {
		console.log(center, oldCenter);
		map.panTo(center);
	}
);

watch(
	() => zoom,
	(zoom) => {
		map.setZoom(zoom);
	}
);
</script>
<template>
	<div :id="id"></div>
</template>
<style scoped>
div {
	height: 90vh;
}
</style>
