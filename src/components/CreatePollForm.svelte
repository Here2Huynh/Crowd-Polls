<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../shared/Button.svelte";
  import PollStore from "../store/PollStore";

  let dispatch = createEventDispatcher();

  let fields = {
    question: "",
    answerA: "",
    answerB: "",
  };
  let errors = {
    question: "",
    answerA: "",
    answerB: "",
  };

  let valid = false;

  const handleSubmit = (e) => {
    valid = true;
    const { question, answerA, answerB } = fields;
    if (question.trim().length < 5) {
      valid = false;
      errors.question = "Question must be at least 5 characters long.";
    } else {
      errors.question = "";
    }

    if (answerA.trim().length < 1) {
      valid = false;
      errors.answerA = "Answer A can not be empty";
    } else {
      errors.answerA = "";
    }

    if (answerB.trim().length < 1) {
      valid = false;
      errors.answerB = "Answer B can not be empty";
    } else {
      errors.answerB = "";
    }

    if (valid) {
      PollStore.update((currentPoll) => {
        return [
          ...currentPoll,
          { ...fields, voteA: 0, voteB: 0, id: Math.random() },
        ];
      });
      dispatch("addPoll");
    }
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
  <div class="form-field">
    <label for="question">Poll question:</label>
    <input type="text" id="question" bind:value={fields.question} />
    <div class="error">{errors.question}</div>
  </div>
  <div class="form-field">
    <label for="answer-a">Answer A:</label>
    <input type="text" id="answer-a" bind:value={fields.answerA} />
    <div class="error">{errors.answerA}</div>
  </div>
  <div class="form-field">
    <label for="answer-b">Answer B:</label>
    <input type="text" id="answer-b" bind:value={fields.answerB} />
    <div class="error">{errors.answerB}</div>
  </div>
  <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  .form-field {
    margin: 18px auto;
  }
  input {
    width: 100%;
    border-radius: 6px;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  .error {
    font-weight: bold;
    font-size: 12px;
    color: #d91b42;
  }
</style>
