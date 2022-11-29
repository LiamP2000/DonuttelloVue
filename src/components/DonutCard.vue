<script setup>

</script>

<template>
    <div class="event-card">
			<h2>Nike</h2>
			<div class="status">
				<span>Status: Done</span>
			</div>
			<img src="/src/assets/donut.png" alt="">
            <h3>nike@hotmail.com</h3>
            <p>18-11-2022</p>
		</div>
  
</template>

<style scoped>
.event-card {
	width: 320px;
	height: auto;
	background: #E72C70;
	border-radius: 20px;
	overflow: hidden;
	padding: 10px 15px;
	margin-bottom: 24px;
	margin-right: 10px;
	transition: all 0.2s linear;
	cursor: pointer;
	color: white;
    margin: auto;
}
img {
	margin-top: 5%;
    width: 100px;
}
.event-card:hover {
	transform: scale(1.01);
	box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2),
		0 1px 15px 0 rgba(0, 0, 0, 0.19);
}

</style>
