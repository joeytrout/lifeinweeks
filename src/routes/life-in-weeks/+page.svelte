<script>
	const years = 91;
	const weeksPerYear = 52;
	let eventName = '';

	const person = {
		birthday: new Date('1982-08-04'),
		events: [
			{ from: '1982-08-04', to: '1982-08-04', event: 'Birth' },
			{ from: '1992-08-04', to: '1992-08-04', event: '10 years old' }
		]
	};

	const lifeGrid = Array(years)
		.fill('')
		.map(() => Array(weeksPerYear).fill(''));

	lifeGrid[0][0] = 'Birth';
	lifeGrid[10][0] = '10 Years Old';
	lifeGrid[20][0] = '20 Years Old';
	lifeGrid[30][0] = '30 Years Old';
	lifeGrid[40][0] = '40 Years Old - Initiate Midlife Crisis';
	lifeGrid[50][0] = '50 Years Old';
	lifeGrid[60][0] = '60 Years Old';
	lifeGrid[70][0] = '70 Years Old';
	lifeGrid[80][0] = '80 Years Old';
	lifeGrid[89][51] = 'Death';
	lifeGrid[90][0] = 'Funeral';
</script>

<h1 class="heading">{eventName || 'Life in Weeks'}</h1>

<div class="grid-container">
	<div class="grid-years">
		<div class="year" />
		<div class="grid-weeks">
			{#each lifeGrid[0] as _, index (index)}
				<div class="week heading" class:gap={(index + 1) % (weeksPerYear / 4) === 0}>
					{index + 1}
				</div>
			{/each}
		</div>
	</div>

	{#each lifeGrid as year, index (index)}
		<div class="grid-years" class:gap={(index + 1) % 10 === 0}>
			<div class="year">{index}</div>
			<div class="grid-weeks">
				{#each year as week, index (index)}
					<div
						class="week data"
						class:has-event={week}
						class:gap={(index + 1) % (weeksPerYear / 4) === 0}
						on:mouseenter={() => (eventName = week)}
						on:mouseleave={() => (eventName = '')}
					/>
				{/each}
			</div>
		</div>
	{/each}
</div>

<style>
	.heading {
		position: sticky;
		top: 0;
	}
	.grid-years {
		display: flex;
	}
	.grid-weeks {
		display: flex;
		line-height: 0;
	}
	.year {
		min-width: 20px;
		height: 10px;
		margin: 1px;
		font-size: xx-small;
		text-align: right;
		margin-right: 5px;
		position: flex;
		align-items: center;
	}
	.week {
		line-height: 0;
		width: 10px;
		height: 10px;
		margin: 1px;
		text-align: center;
		font-size: xx-small;
	}
	.week.data {
		background-color: white;
		line-height: 0;
	}

	.week.has-event {
		background-color: green;
	}
	.grid-years.gap {
		margin-bottom: 10px;
	}
	.week.gap {
		margin-right: 10px;
	}
</style>
