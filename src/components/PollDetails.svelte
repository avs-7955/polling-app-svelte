<script>
	import PollStore from "../stores/PollStore"
	import Card from "../shared/Card.svelte"
	import Button from "../shared/Button.svelte"
	import { tweened } from "svelte/motion"
	export let poll

	// reactive value
	$: totalVotes = poll.votesA + poll.votesB

	$: percentA = Math.floor((100 / totalVotes) * poll.votesA) || 0
	$: percentB = Math.floor((100 / totalVotes) * poll.votesB) || 0

	// tweened values for percentages
	const tweenA = tweened(0)
	const tweenB = tweened(0)
	$: tweenA.set(percentA)
	$: tweenB.set(percentB)
	// $: console.log($tweenA, $tweenB)

	// increasing votes upon click
	const handleVote = (option, id) => {
		PollStore.update((currentPolls) => {
			let copiedPolls = [...currentPolls]
			let upvotedPoll = copiedPolls.find((poll) => poll.id === id)
			if (option == "a") upvotedPoll.votesA += 1
			if (option == "b") upvotedPoll.votesB += 1

			return copiedPolls
		})
	}

	// deleting poll
	const handleDelete = (id) => {
		PollStore.update((currentPolls) => {
			let copiedPolls = [...currentPolls]
			copiedPolls = copiedPolls.filter((poll) => poll.id != id)
			return copiedPolls
		})
	}
</script>

<Card>
	<div class="poll">
		<h3>{poll.question}</h3>
		<p>
			Total votes: {totalVotes}
		</p>
		<div class="answer" on:click={() => handleVote("a", poll.id)}>
			<div class="percent percent-a" style="width: {$tweenA}%">
				<span>{poll.answerA}({poll.votesA})</span>
			</div>
		</div>
		<div class="answer" on:click={() => handleVote("b", poll.id)}>
			<div class="percent percent-b" style="width: {$tweenB}%">
				<span>{poll.answerB}({poll.votesB})</span>
			</div>
		</div>
	</div>
	<div class="delete">
		<Button
			flat={true}
			on:click={() => {
				handleDelete(poll.id)
			}}>Delete</Button
		>
	</div>
</Card>

<style>
	h3 {
		margin: 0 auto;
		color: #555;
	}
	p {
		margin-top: 6px;
		font-size: 14px;
		color: #aaa;
		margin-bottom: 30px;
	}
	.answer {
		background: #fafafa;
		cursor: pointer;
		margin: 10px auto;
		position: relative;
	}
	.answer:hover {
		opacity: 0.6;
	}
	span {
		display: inline-block;
		padding: 10px 20px;
	}
	.percent {
		height: 100%;
		/* position: absolute; */
		box-sizing: border-box;
		border-radius: 6px;
	}
	.percent-a {
		background-color: rgba(217, 27, 66, 0.2);
		border-left: 4px solid #d91b42;
	}
	.percent-b {
		/* background-color: rgba(69, 196, 150, 0.2); */
		background-color: rgba(255, 215, 130, 0.5);
		/* border-left: 4px solid #45c496; */
		border-left: 4px solid #ffd782;
	}
	/* delete button */
	.delete {
		text-align: center;
		margin-top: 30px;
	}
</style>
