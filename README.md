<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>audiobiotic // nature_tech</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'bio-green': '#457053',
                        'bio-dark': '#2c4735',
                        'bio-light': '#6c9e7e',
                        'glass': 'rgba(255, 255, 255, 0.1)',
                        'glass-border': 'rgba(255, 255, 255, 0.2)',
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        mono: ['Courier New', 'Courier', 'monospace'],
                    },
                    letterSpacing: {
                        widest: '.25em',
                        y2k: '.3em',
                    }
                }
            }
        }
    </script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700;900&display=swap');

        body {
            background-color: #457053; 
            color: #ffffff;
            overflow: hidden; 
        }

        .bg-grid {
            background-size: 50px 50px;
            background-image: 
                linear-gradient(to right, rgba(255, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(to bottom, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
            mask-image: radial-gradient(circle at center, black 30%, transparent 90%);
            -webkit-mask-image: radial-gradient(circle at center, black 30%, transparent 90%);
        }

        .liquid-blob {
            position: absolute;
            filter: blur(40px);
            border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
            animation: morph 15s ease-in-out infinite, spin 25s linear infinite;
            z-index: 0;
            opacity: 0.4;
        }

        .blob-1 { 
            width: 50vw; height: 50vw; top: -10%; left: -10%; 
            background: radial-gradient(circle at 30% 30%, #6c9e7e, transparent);
        }
        .blob-2 { 
            width: 40vw; height: 40vw; bottom: -10%; right: -10%; 
            animation-delay: -7s; 
            background: radial-gradient(circle at 70% 70%, #ffffff, transparent);
            opacity: 0.15;
        }

        @keyframes morph {
            0%, 100% { border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%; }
            34% { border-radius: 70% 30% 50% 50% / 30% 30% 70% 70%; }
            67% { border-radius: 100% 60% 60% 100% / 100% 100% 60% 60%; }
        }

        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-12px); }
        }
        .biotic-float {
            animation: float 6s ease-in-out infinite;
        }

        .glass-panel {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
        }

        .reverb-btn {
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .reverb-btn.active {
            background: rgba(255, 255, 255, 0.2);
            border-color: rgba(255, 255, 255, 0.8);
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.3);
        }

        .reverb-btn::after {
            content: '';
            position: absolute;
            top: 50%; left: 50%;
            width: 0; height: 0;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.4s ease, height 0.4s ease;
        }

        .reverb-btn.active::after {
            width: 150%; height: 150%;
        }

        .play-btn {
            transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
        }
        .play-btn:hover {
            transform: scale(1.05);
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 0 25px rgba(255, 255, 255, 0.2);
        }
        .play-btn:active {
            transform: scale(0.98);
        }
    </style>
</head>

<body class="flex items-center justify-center min-h-screen relative font-sans">

    <div class="absolute inset-0 bg-grid z-0"></div>
    <div class="liquid-blob blob-1"></div>
    <div class="liquid-blob blob-2"></div>

    <main class="relative z-10 flex flex-col items-center w-full max-w-2xl px-6">
        
        <!-- ========================================================================= -->
        <!-- ======================= USER LOGO IMAGE PATH ============================ -->
        <!-- ========================================================================= -->
        <!-- EDIT THE 'src' ATTRIBUTE BELOW TO POINT TO YOUR LOGO FILE PATH            -->
        <!-- Current Logo: 2.png                                                       -->
        <!-- ========================================================================= -->
        <div class="mb-10 flex flex-col items-center w-full drop-shadow-lg biotic-float">
            <div class="relative w-full max-w-[250px] flex justify-center">
                <img 
                    src="2.png" 
                    alt="Audiobiotic Logo" 
                    class="w-full h-auto object-contain drop-shadow-[0_0_25px_rgba(255,255,255,0.15)]" 
                >
            </div>
        </div>
        <!-- ========================================================================= -->
        <!-- ===================== END USER LOGO IMAGE PATH ========================== -->
        <!-- ========================================================================= -->
        
        <div class="flex items-center gap-4 mb-8 opacity-80">
            <div class="w-12 h-[1px] bg-white opacity-50"></div>
            <p class="font-mono text-xs tracking-widest uppercase">
                convolution_reverb // env_sim
            </p>
            <div class="w-12 h-[1px] bg-white opacity-50"></div>
        </div>

        <div class="glass-panel rounded-2xl p-6 w-full max-w-md mb-8">
            <p class="font-mono text-xs text-center mb-4 opacity-70 tracking-widest uppercase">Select Acoustic Environment</p>
            <div class="flex justify-between gap-3" id="reverb-controls">
                <button class="reverb-btn active flex-1 py-3 rounded-xl border border-glass-border font-sans font-bold text-sm" data-env="forest">
                    Forest
                </button>
                <button class="reverb-btn flex-1 py-3 rounded-xl border border-glass-border font-sans font-bold text-sm" data-env="cave">
                    Cave
                </button>
                <button class="reverb-btn flex-1 py-3 rounded-xl border border-glass-border font-sans font-bold text-sm" data-env="digital">
                    Digital
                </button>
            </div>
        </div>

        <button id="play-btn" class="play-btn glass-panel px-12 py-5 rounded-full font-mono text-sm tracking-y2k uppercase flex items-center gap-4 group text-white border border-white/40">
            <span class="w-2.5 h-2.5 rounded-full bg-white group-hover:animate-ping"></span>
            Initialize_Audio
            <span class="w-2.5 h-2.5 rounded-full bg-white group-hover:animate-ping"></span>
        </button>

        <div id="status-display" class="font-mono text-xs mt-6 h-4 opacity-0 transition-opacity duration-300">
            [ waiting for input ]
        </div>
    </main>

    <script>
        let currentEnvironment = 'forest';
        let isPlaying = false;

        const reverbBtns = document.querySelectorAll('.reverb-btn');
        reverbBtns.forEach(btn => {
            btn.addEventListener('click', (e) => {
                reverbBtns.forEach(b => b.classList.remove('active'));
                e.target.classList.add('active');
                currentEnvironment = e.target.getAttribute('data-env');
                document.getElementById('status-display').style.opacity = 1;
                document.getElementById('status-display').innerText = `[ env set: ${currentEnvironment} ]`;
                setTimeout(() => document.getElementById('status-display').style.opacity = 0, 2000);
            });
        });

        const environments = {
            forest:  { decay: 3.5, duration: 1.5, filterType: 'bandpass', filterFreq: 1500, mix: 0.5 },
            cave:    { decay: 1.5, duration: 4.0, filterType: 'lowpass',  filterFreq: 600,  mix: 0.8 },
            digital: { decay: 8.0, duration: 1.0, filterType: 'highpass', filterFreq: 2500, mix: 0.6 }
        };

        function generateImpulseResponse(ctx, duration, decay) {
            const sampleRate = ctx.sampleRate;
            const length = sampleRate * duration;
            const impulse = ctx.createBuffer(2, length, sampleRate);
            
            const left = impulse.getChannelData(0);
            const right = impulse.getChannelData(1);

            for (let i = 0; i < length; i++) {
                const n = length - i;
                const envelope = Math.pow(n / length, decay);
                left[i] = (Math.random() * 2 - 1) * envelope * 0.5;
                right[i] = (Math.random() * 2 - 1) * envelope * 0.5;
            }
            return impulse;
        }

        function playPluck(ctx, time, freq, destination) {
            const osc = ctx.createOscillator();
            const gainNode = ctx.createGain();
            
            osc.type = 'sine';
            osc.frequency.setValueAtTime(freq, time);
            
            gainNode.gain.setValueAtTime(0, time);
            gainNode.gain.linearRampToValueAtTime(0.6, time + 0.02);
            gainNode.gain.exponentialRampToValueAtTime(0.001, time + 0.5);

            osc.connect(gainNode);
            gainNode.connect(destination);

            osc.start(time);
            osc.stop(time + 0.6);
        }

        document.getElementById('play-btn').addEventListener('click', async () => {
            if (isPlaying) return;
            isPlaying = true;

            const status = document.getElementById('status-display');
            status.style.opacity = 1;
            status.innerText = "[ synthesizing impulse response... ]";

            const AudioContext = window.AudioContext || window.webkitAudioContext;
            const ctx = new AudioContext();
            
            const env = environments[currentEnvironment];

            const mainOut = ctx.createGain(); 
            const dryGain = ctx.createGain();
            dryGain.gain.value = 1.0 - (env.mix * 0.5);

            const wetGain = ctx.createGain();
            wetGain.gain.value = env.mix;

            const convolver = ctx.createConvolver();
            convolver.buffer = generateImpulseResponse(ctx, env.duration, env.decay);

            const revFilter = ctx.createBiquadFilter();
            revFilter.type = env.filterType;
            revFilter.frequency.value = env.filterFreq;

            mainOut.connect(dryGain);
            dryGain.connect(ctx.destination);

            mainOut.connect(convolver);
            convolver.connect(revFilter);
            revFilter.connect(wetGain);
            wetGain.connect(ctx.destination);

            status.innerText = `[ applying ${currentEnvironment} convolution ]`;

            const r = 432;
            const M3 = r * 1.25; 
            const P5 = r * 1.5;  
            const O = r * 2;     
            const hM3 = r * 2.5;

            const melody = [
                { freq: r,   delay: 0.0 },
                { freq: M3,  delay: 0.15 },
                { freq: P5,  delay: 0.3 },
                { freq: O,   delay: 0.45 },
                { freq: P5,  delay: 0.7 },
                { freq: O,   delay: 0.85 },
                { freq: hM3, delay: 1.0 }
            ];

            const startTime = ctx.currentTime + 0.1;
            
            melody.forEach(note => {
                playPluck(ctx, startTime + note.delay, note.freq, mainOut);
            });

            const lastNoteTime = melody[melody.length - 1].delay * 1000;
            setTimeout(() => {
                status.innerText = "[ playback complete ]";
                setTimeout(() => status.style.opacity = 0, 1500);
                isPlaying = false;
            }, lastNoteTime + (env.duration * 1000) + 500);
        });
    </script>
</body>
</html>
