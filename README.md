<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>STAR-KITTEN: THE ORACLE</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Major+Mono+Display&family=Space+Grotesk:wght@300;700&display=swap');

        :root {
            --neon: #ff0033;
            --glass: rgba(255, 255, 255, 0.05);
            --border: rgba(255, 0, 51, 0.4);
        }

        body {
            margin: 0; padding: 0;
            background: #000;
            color: #fff;
            font-family: 'Space Grotesk', sans-serif;
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
        }

        /* Stage */
        #stage {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            position: relative;
            background: radial-gradient(circle at center, #1a0000 0%, #000 100%);
        }

        .cat-vibe {
            font-size: 100px;
            filter: drop-shadow(0 0 20px var(--neon));
            transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 2;
        }

        #oracle-bubble {
            font-family: 'Major Mono Display', monospace;
            color: var(--neon);
            font-size: 0.85rem;
            margin-top: 20px;
            text-align: center;
            padding: 15px;
            max-width: 80%;
            min-height: 40px;
            border: 1px solid transparent;
            transition: 0.3s;
        }

        .bubble-active {
            border: 1px solid var(--border);
            background: var(--glass);
            border-radius: 10px;
        }

        /* UI Layer */
        #ui-layer {
            background: #0a0a0a;
            padding: 20px;
            border-top: 1px solid var(--border);
            transition: 0.5s ease;
        }

        .chat-container {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        #chat-input {
            flex: 1;
            background: #111;
            border: 1px solid var(--border);
            color: #fff;
            padding: 12px;
            border-radius: 8px;
            font-family: 'Space Grotesk';
            outline: none;
        }

        .send-btn {
            background: var(--neon);
            color: #000;
            border: none;
            padding: 0 15px;
            border-radius: 8px;
            font-weight: bold;
        }

        .track-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
        }

        .track-btn {
            background: var(--glass);
            border: 1px solid var(--border);
            color: white;
            padding: 12px 5px;
            border-radius: 8px;
            font-size: 0.75rem;
            text-align: center;
            text-transform: uppercase;
        }

        /* Ghost Mode */
        body.ghost-mode #ui-layer { transform: translateY(110%); }
        .ghost-toggle { position: absolute; top: 20px; right: 20px; font-size: 1.2rem; opacity: 0.5; }

        #player-container { display: none; }
    </style>
</head>
<body id="main-body">

    <main id="stage" onclick="checkExitGhost()">
        <div class="ghost-toggle" onclick="toggleGhost()">📷</div>
        <div class="cat-vibe" id="cat">🐈‍⬛</div>
        <div id="oracle-bubble">W H A T . D O . Y O U . W A N T ?</div>
    </main>

    <aside id="ui-layer">
        <div class="chat-container">
            <input type="text" id="chat-input" placeholder="Talk to the Star-Kitten...">
            <button class="send-btn" onclick="askOracle()">ASK</button>
        </div>

        <div class="track-grid">
            <div class="track-btn" onclick="playTrack('fHI8X4OXskQ', 'Blinding Lights', '😎')">🚨 LIGHTS</div>
            <div class="track-btn" onclick="playTrack('34Na4j8AVgA', 'Starboy', '⚡')">⚡ STARBOY</div>
            <div class="track-btn" onclick="playTrack('XXYlFuWEuKI', 'Save Your Tears', '💧')">💧 TEARS</div>
            <div class="track-btn" onclick="playTrack('YvVvU_R403I', 'The Hills', '🩸')">🌆 THE HILLS</div>
        </div>

        <div id="player-container">
            <iframe id="video-player" width="1" height="1" src="" frameborder="0" allow="autoplay"></iframe>
        </div>
    </aside>

<script>
    const lyrics = [
        "I only call you when it's half past five",
        "I'm just tryna get you in the mood",
        "I said ooh, I'm blinded by the lights",
        "Look what you've done...",
        "I don't know why I run away",
        "Never need a bitch, I'm what a bitch need",
        "Save your tears for another day",
        "I'm a Starboy.",
        "When I'm fucked up, that's the real me"
    ];

    const moods = ['😎', '😵‍💫', '🩸', '🔥', '🍷'];

    function askOracle() {
        const input = document.getElementById('chat-input');
        const bubble = document.getElementById('oracle-bubble');
        const cat = document.getElementById('cat');

        if(input.value.trim() === "") return;

        // Logic
        const reply = lyrics[Math.floor(Math.random() * lyrics.length)];
        const mood = moods[Math.floor(Math.random() * moods.length)];

        bubble.innerText = reply.toUpperCase();
        bubble.classList.add('bubble-active');
        cat.innerText = mood;
        input.value = "";

        if ("vibrate" in navigator) navigator.vibrate([50, 50, 50]);

        cat.style.transform = "scale(1.3)";
        setTimeout(() => cat.style.transform = "scale(1)", 200);
    }

    function playTrack(videoId, title, mood) {
        document.getElementById('video-player').src = `https://www.youtube.com/embed/${videoId}?autoplay=1&controls=0`;
        document.getElementById('oracle-bubble').innerText = title.toUpperCase();
        document.getElementById('cat').innerText = mood;
    }

    function toggleGhost() { document.getElementById('main-body').classList.add('ghost-mode'); }
    function checkExitGhost() { document.getElementById('main-body').classList.remove('ghost-mode'); }

    // Handle Enter Key
    document.getElementById('chat-input').addEventListener("keypress", function(event) {
        if (event.key === "Enter") askOracle();
    });
</script>

</body>
</html>
