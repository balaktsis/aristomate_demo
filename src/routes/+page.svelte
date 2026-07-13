<script>
	import { universisFetch } from '$lib/universis_fetch';

	let courses = [];

	async function getGrades() {
		const result = await universisFetch("students/me/courses");
		courses = result.value;

		console.log(courses);
	}

	let section = "notes";


	let tasks = [];
	let newtask;


</script>


<ion-header>
	<ion-toolbar>
		<ion-title>Universis</ion-title>
	</ion-toolbar>
	<ion-segment on:ionChange={(event) => section = event.detail.value }>
		<ion-segment-button value="grades">
			<ion-label>Grades</ion-label>
		</ion-segment-button>
		<ion-segment-button value="notes">
			<ion-label>Notes</ion-label>
		</ion-segment-button>
	</ion-segment>
</ion-header>


<ion-content>
	{#if section == "grades"}
		<ion-card>
			<p>Here are my grades.</p>
			<ion-button on:click={() => getGrades()}>Load my courses</ion-button>
		</ion-card>
		
		{#if courses.length == 0}
			<ion-card>No courses found.</ion-card>
		{:else}
			<ion-list>
				{#each courses as course}
				<ion-item>
					<ion-label>Titlos: {course.courseTitle}</ion-label>
					{#if course.formattedGrade }
					<ion-text>Bathmos: {course.formattedGrade}</ion-text>
					{:else}
					<ion-text>Bathmos: No grade yet</ion-text>
					{/if}
				</ion-item>
				{/each}
			</ion-list>
		{/if}
	
	
	
	{:else if section == "notes"}
	<ion-card>
		<ion-card-header>
			My ToDo list
		</ion-card-header>
		<ion-input
			placeholder="Add a task"
			label="Title"
			value={newtask}
			on:ionInput={(event) => {newtask = event.detail.value}}>
		</ion-input>
		<ion-button on:click={() => {tasks = [...tasks, newtask];}}>Add</ion-button>
		<ion-list>
			{#each tasks as task}
			<ion-item>
				<ion-label>{task}</ion-label>
			</ion-item>
			{/each}
		</ion-list>


	</ion-card>
	{/if}
</ion-content>

<ion-footer>
<ion-toolbar>
	<ion-label>This is a footer!</ion-label>
</ion-toolbar>
</ion-footer>
  