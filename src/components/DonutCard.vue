<script setup>

</script>

<template>
    <!--<div class="card">
			<h2 class="card__company">Nike</h2>
			<div class="card__status">
				<span>Status: Done</span>
			</div>
			<div class="">
				<p>Glazuur:</p>
				<p>Topping:</p>
				<p>Logo:</p>
			</div>
			
			<img class="card__img" src="/src/assets/donut.png" alt="">
            <h3 class="card__email">nike@hotmail.com</h3>
            <p class="card__date">18-11-2022</p>
		</div>-->
	
		<div class="card">
			<div class="card__amount">
				<p class="card__title">Amount:</p>
				<p class="card__amountNumber">8</p>
			</div>
			<div class="card__donut">
				<img class="card__img" src="/src/assets/donut.png" alt="">
			</div>
			<div class="card__description">
				<p class="card__title">Description:</p>
				<p class="card__input">Contacteer me via gsm indien ik niet antwoord via mail</p>
				
			</div>
			<div class="card__email">
				<p class="card__title">E-mail:</p>
				<p class="card__input">nike@hotmail.com</p>
			</div>
			<div class="card__duedate">
				<p class="card__title">Due date:</p>
				<p class="card__input">19-11-2022</p>
			</div>
			<div class="card__company">Nike</div>
			<div class="card__creationdate"></div>
			<div class="card__ingredients">
				<p><span class="card__title">Glazuur: </span>Chocolate </p>
				<p><span class="card__title">Topping: </span>Oreo</p>
				<p><span class="card__title">Logo: </span>Logo.png</p>
				
			</div>
		</div>
  
</template>

<style scoped>
.card {
	width: 320px;
	height: auto;
	background: var(--primary-pink);
	border-radius: 20px;
	overflow: hidden;
	padding: 10px 15px;
	margin-bottom: 24px;
	margin-right: 10px;
	transition: all 0.2s linear;
	cursor: pointer;
	color: var(--neutral);
    margin: auto;
	padding: 20px;
	margin: 10px;
}
.card__img {
	margin-top: 5%;
    width: 100px;
}
.card:hover {
	transform: scale(1.01);
	box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2),
		0 1px 15px 0 rgba(0, 0, 0, 0.19);
}

.card {
  display: grid; 
  grid-template-columns: 0.5fr 0.5fr 0.5fr; 
  grid-template-rows: 0.5fr 0.5fr 0.5fr 0.5fr 0.5fr 0.5fr; 
  gap: 0px 0px; 
  
}

.card__company { 
	grid-area: 1 / 1 / 2 / 4;
	font-weight: 700;
	font-size: 2em;
	margin-top: 0.3em;
 }
.card__creationdate { grid-area: 1 / 3 / 2 / 4; }
.card__email { 
	grid-area: 6 / 1 / 7 / 3;

}
.card__duedate { 
	grid-area: 6 / 3 / 7 / 4;
 }
.card__description { 
	grid-area: 5 / 1 / 6 / 4;
	
 }
.card__amount { grid-area: 4 / 3 / 5 / 4; }

.card__amountNumber { 
	text-align: left;
	font-size: 1.5em;
	font-weight: 700;
	margin-left: 1em;
}
.card__ingredients { 
	grid-area: 4 / 1 / 5 / 3;
	text-align: left;
 }
.card__donut { grid-area: 2 / 1 / 4 / 4; }

.card__title {
	text-align: left;
	font-weight: 600;
	margin-left: 0.3em;
}

.card__input{
	text-align: left;
	margin-left: 0.3em;
}



</style>
