<script>
    //import mic from '/assets/mic.png';
    import { onMount } from "svelte";

    const randomNum = getRandomNumber();
    let msg = "";
    console.log(randomNum);

    onMount(() => {
        window.SpeechRecognition =
            window.SpeechRecognition || window.webkitSpeechRecognition;

        let recognition = new window.SpeechRecognition();

        recognition.start();

        // Speak result
        recognition.addEventListener("result", onSpeak);

        // End SR service
        recognition.addEventListener("end", () => recognition.start());
    });

    function onSpeak(e) {
        console.log("on speak");
        const recognized = e.results[0][0].transcript;
        console.log(recognized);
        msg = recognized;
    }

    function getRandomNumber() {
        return Math.floor(Math.random() * 100) + 1;
    }
</script>

<h1>Guess a Number Between 1 - 100</h1>

<h3>Speak the number into your microphone</h3>

<div id="msg" class="msg">
    <div>You said:</div>
    <span class="box">{msg}</span>
</div>
