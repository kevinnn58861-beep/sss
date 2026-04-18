<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Saturnus v5: Cosmic Architect (GPGPU Shaders)</title>
    <style>
        body { margin: 0; overflow: hidden; background: #000; color: #fff; font-family: 'Segoe UI', sans-serif; }
        #ui { position: absolute; top: 30px; left: 30px; z-index: 10; border-left: 2px solid #00ffff; padding-left: 15px; pointer-events: none; text-shadow: 0 0 5px rgba(0,255,255,0.5); }
        h1 { margin: 0; font-weight: 200; letter-spacing: 4px; font-size: 18px; color: #00ffff; }
        #status { font-size: 12px; opacity: 0.8; margin-top: 5px; color: #aaa; }
        .instruksi { font-size: 10px; color: #555; margin-top: 10px; line-height: 1.5; }
        
        #video-container { position: absolute; bottom: 20px; right: 20px; width: 180px; height: 135px; transform: scaleX(-1); border-radius: 12px; overflow: hidden; border: 1px solid rgba(0,255,255,0.2); box-shadow: 0 5px 15px rgba(0,0,0,0.5); opacity: 0.6; }
        #input_video { display: none; }
        #output_canvas { width: 100%; height: 100%; object-fit: cover; }
    </style>
</head>
<body>
    <div id="ui">
        <h1>SATURNUS v5 [ARCHITECT]</h1>
        <p id="status">Menginisialisasi GPU...</p>
        <div class="instruksi">
            [Dua Tangan Disarankan]<br>
            - Kanan (R) Telapak: Gerakkan Saturnus<br>
            - Kiri (L) Jempol+Kelingking: Zoom<br>
            - Kiri (L) Telunjuk: SUPERNOVA!<br>
            - Kiri (L) Tengah: Menara Eiffel<br>
            - Kiri (L) Manis: Roket Kosmik
        </div>
    </div>
    <video id="input_video"></video>
    <div id="video-container"><canvas id="output_canvas"></canvas></div>

    <script src="https://cdn.jsdelivr.net/npm/@mediapipe/hands@0.4/hands.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils@0.3/camera_utils.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/mrdoob/three.js@r128/examples/js/misc/GPUComputationRenderer.js"></script>

    <script id="computeShaderPosition" type="x-shader/x-fragment">
        uniform float time;
        uniform float delta;
        uniform vec3 handGravityPos; // Tangan Kanan
        uniform int morphState;       // Tangan Kiri: 0=Saturn, 1=Supernova, 2=Eiffel, 3=Rocket
        uniform float supernovaForce;

        // Fungsi acak sederhana
        float rand(vec2 co){ return fract(sin(dot(co.xy ,vec2(12.9898,78.233))) * 43758.5453); }

        void main() {
            vec2 uv = gl_FragCoord.xy / resolution.xy;
            vec4 tmpPos = texture2D( texturePosition, uv );
            vec3 pos = tmpPos.xyz;
            float type = tmpPos.w; // 0=Planet, 1=Ring

            // Data Awal (Saturnus)
            vec3 originalPos = texture2D( texturePosition, uv ).xyz; 

            // Target Posisi untuk Morphing
            vec3 targetPos = originalPos; 

            // --- LOGIKA MORPHING & FISIKA ---
            
            if(morphState == 1) { // SUPERNOVA (Meledak)
                vec3 dirFromCenter = normalize(pos + vec3(rand(uv), rand(uv*2.0), rand(uv*3.0))*0.1 );
                pos += dirFromCenter * supernovaForce * delta * (20.0 + rand(uv)*10.0); // Kecepatan acak
            } 
            else if(morphState == 2) { // MENARA EIFFEL (Kisi Fraktal)
                float h = 15.0; // Tinggi
                float baseW = 4.0; // Lebar bawah
                float z_eiffel = (rand(uv) - 0.5) * h; // Posisi vertikal acak
                float taper = baseW * (1.0 - (z_eiffel + h/2.0)/h); // Mengerucut ke atas
                float spread = (rand(uv*1.5) - 0.5) * taper * 1.5;
                
                // Membuat struktur kisi fraktal sederhana
                if(mod(z_eiffel, 2.0) < 0.1 || mod(spread, 1.0) < 0.05) {
                     targetPos = vec3(spread, spread * (rand(uv*2.0)-0.5), z_eiffel);
                } else {
                     targetPos = vec3(spread * 0.2, spread * 0.1, z_eiffel); // Isi dalam
                }
            }
            else if(morphState == 3) { // ROCKET (Silinder + Kerucut)
                float rocketHeight = 12.0;
                float rocketRadius = 1.2;
                float z_rocket = (rand(uv) - 0.5) * rocketHeight;
                float angle = rand(uv*2.0) * 3.14159 * 2.0;

                if(z_rocket > rocketHeight * 0.3) { // Bagian Kerucut Atas
                    float coneTaper = rocketRadius * (1.0 - (z_rocket - rocketHeight*0.3)/(rocketHeight*0.2));
                    targetPos = vec3(cos(angle)*coneTaper, sin(angle)*coneTaper, z_rocket);
                } else { // Bagian Silinder Badan
                    targetPos = vec3(cos(angle)*rocketRadius, sin(angle)*rocketRadius, z_rocket);
                    // Sirip bawah
                    if(z_rocket < -rocketHeight * 0.4 && mod(angle, 3.14159/2.0) < 0.2) {
                        targetPos.x *= 2.5; targetPos.y *= 2.5;
                    }
                }
            }
            else { // SATURNUS DEFAULT
                targetPos = originalPos;
            }

            // --- APLIKASIKAN GERAKAN ---
            
            if(morphState != 1) {
                // Gravitasi Tangan Kanan (Ditarik halus ke telapak)
                vec3 dirToHand = handGravityPos - pos;
                float distToHand = length(dirToHand);
                if(distToHand > 0.1) {
                    pos += normalize(dirToHand) * (0.05 / (distToHand + 1.0));
                }

                // Tarikan kembali ke target bentuk (Gravity/Implosion)
                vec3 dirToTarget = targetPos - pos;
                float distToTarget = length(dirToTarget);
                if(distToTarget > 0.01) {
                    pos += dirToTarget * 0.04; // Kecepatan menyatu
                }
            }

            // Sedikit rotasi alami Saturnus (jika bukan supernova)
            if(morphState == 0) {
                float rotAngle = 0.003 * delta * (type == 1.0 ? 2.0 : 1.0); 
                mat3 rotY = mat3(cos(rotAngle), 0.0, sin(rotAngle), 0.0, 1.0, 0.0, -sin(rotAngle), 0.0, cos(rotAngle));
                pos = rotY * pos;
            }

            gl_FragColor = vec4( pos, type );
        }
    </script>

    <script id="particleVertexShader" type="x-shader/x-vertex">
        uniform sampler2D texturePosition;
        uniform float time;
        uniform int morphState;
        varying vec4 vColor;
        varying float vOpacity;

        void main() {
            vec4 tmpPos = texture2D( texturePosition, uv );
            vec3 pos = tmpPos.xyz;
            float type = tmpPos.w; // Planet (0) atau Ring (1)

            // Warna Kosmik Gradasi
            vec3 colorSphereCore = vec3(1.0, 0.9, 0.3); // Gold
            vec3 colorSphereOuter = vec3(0.5, 0.0, 0.5); // Purple Deep
            vec3 colorRingInner = vec3(0.0, 1.0, 1.0);   // Cyan
            vec3 colorRingOuter = vec3(1.0, 0.0, 1.0);   // Magenta

            float distFromCenter = length(pos);
            vec3 finalColor;

            if(type == 0.0) { // PLANET
                finalColor = mix(colorSphereCore, colorSphereOuter, smoothstep(0.0, 4.5, distFromCenter));
            } else { // RING
                finalColor = mix(colorRingInner, colorRingOuter, smoothstep(5.5, 11.0, distFromCenter));
            }

            // Efek Supernova: Putih Panas lalu memudar
            if(morphState == 1) {
                finalColor = mix(finalColor, vec3(1.0), smoothstep(10.0, 30.0, distFromCenter));
                vOpacity = 1.0 - smoothstep(20.0, 50.0, distFromCenter); // Memudar saat menjauh
            } else {
                vOpacity = 0.9;
            }
            
            vColor = vec4(finalColor, vOpacity);

            // Ukuran partikel dinamis (pulsing + depth)
            vec4 mvPosition = modelViewMatrix * vec4( pos, 1.0 );
            gl_PointSize = (12.0 / -mvPosition.z) * (1.0 + 0.3 * sin(time * 4.0 + pos.x));
            gl_Position = projectionMatrix * mvPosition;
        }
    </script>

    <script id="particleFragmentShader" type="x-shader/x-fragment">
        varying vec4 vColor;
        varying float vOpacity;
        
        void main() {
            // Membuat bentuk lingkaran kustom (soft glow)
            float dist = length(gl_PointCoord - vec2(0.5));
            if (dist > 0.5) discard; 

            // Gradien glow lembut
            float alpha = 1.0 - smoothstep(0.0, 0.5, dist);
            gl_FragColor = vec4(vColor.rgb, vColor.a * alpha * vOpacity);
        }
    </script>

    <script>
        // --- CONFIG ---
        const WIDTH = 256; // Jumlah Partikel = WIDTH * WIDTH (~65,536)
        const PARTICLES = WIDTH * WIDTH;
        const PARAMS = {
            planetRadius: 4,
            ringInnerRadius: 5.8,
            ringOuterRadius: 11,
            supernovaForce: 0.18
        };

        // --- THREE.JS SETUP ---
        const scene = new THREE.Scene();
        scene.fog = new THREE.FogExp2(0x000000, 0.006); 

        const camera = new THREE.PerspectiveCamera(65, window.innerWidth / window.innerHeight, 0.1, 2000);
        camera.position.set(0, 5, 25);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(window.devicePixelRatio);
        document.body.appendChild(renderer.domElement);

        const mainGroup = new THREE.Group(); // Wadah Saturnus
        scene.add(mainGroup);

        // --- GPGPU SETUP ---
        const gpuCompute = new THREE.GPUComputationRenderer(WIDTH, WIDTH, renderer);
        
        // Buat tekstur posisi awal (Saturnus)
        const dtPosition = gpuCompute.createTexture();
        fillPositionTexture(dtPosition);

        // Tambahkan shader computation
        const positionVariable = gpuCompute.addVariable("texturePosition", document.getElementById('computeShaderPosition').textContent, dtPosition);
        
        // Set Uniforms (Data dari JS ke Shader)
        positionVariable.material.uniforms.time = { value: 0.0 };
        positionVariable.material.uniforms.delta = { value: 0.0 };
        positionVariable.material.uniforms.handGravityPos = { value: new THREE.Vector3(0,0,0) };
        positionVariable.material.uniforms.morphState = { value: 0 }; // Default Saturnus
        positionVariable.material.uniforms.supernovaForce = { value: PARAMS.supernovaForce };

        // Inisialisasi GPGPU
        const error = gpuCompute.init();
        if (error !== null) { console.error(error); }


        // --- PARTICLE OBJECT SETUP (Menggunakan Shaders Kustom) ---
        const geometry = new THREE.BufferGeometry();
        const uvs = new Float32Array(PARTICLES * 2);
        
        // Isi UV agar setiap partikel tahu koordinat tekstur GPGPU-nya
        for (let i = 0; i < PARTICLES; i++) {
            uvs[i * 2] = (i % WIDTH) / WIDTH;
            uvs[i * 2 + 1] = Math.floor(i / WIDTH) / WIDTH;
        }
        geometry.setAttribute('uv', new THREE.BufferAttribute(uvs, 2));
        geometry.setAttribute('position', new THREE.BufferAttribute(new Float32Array(PARTICLES * 3), 3)); // Placeholder

        const particleMaterial = new THREE.ShaderMaterial({
            uniforms: {
                texturePosition: { value: null }, // Diisi hasil GPGPU
                time: { value: 0.0 },
                morphState: { value: 0 }
            },
            vertexShader: document.getElementById('particleVertexShader').textContent,
            fragmentShader: document.getElementById('particleFragmentShader').textContent,
            blending: THREE.AdditiveBlending, // Efek glowing
            transparent: true,
            depthWrite: false
        });

        const particleSystem = new THREE.Points(geometry, particleMaterial);
        particleSystem.rotation.x = Math.PI / 6; // Kemiringan ikonik
        mainGroup.add(particleSystem);


        // --- LOGIKA SENSOR DUA TANGAN (MEDIAPIPE) ---
        let handStatus = "Mencari Tangan...";
        let handGravityPos = new THREE.Vector3(0,0,0);
        let morphState = 0; // 0=Saturn, 1=Supernova, 2=Eiffel, 3=Rocket
        let targetCameraZ = 25;

        const hands = new Hands({locateFile: (file) => `https://cdn.jsdelivr.net/npm/@mediapipe/hands@0.4/${file}`});
        hands.setOptions({ maxNumHands: 2, modelComplexity: 1, minDetectionConfidence: 0.8 });

        hands.onResults(res => {
            const statusEl = document.getElementById('status');
            let rightDetected = false;
            let leftDetected = false;

            if (res.multiHandLandmarks && res.multiHandLandmarks.length > 0) {
                res.multiHandLandmarks.forEach((marks, index) => {
                    const label = res.multiHandedness[index].label; // "Left" atau "Right"

                    if (label === "Right") {
                        // TANGAN KANAN: Gerakkan Saturnus (Gravitasi Kustom di Shader)
                        handGravityPos.x = (marks[0].x - 0.5) * 35;
                        handGravityPos.y = -(marks[0].y - 0.5) * 25;
                        handGravityPos.z = (marks[0].z) * 15;
                        rightDetected = true;
                    }

                    if (label === "Left") {
                        // TANGAN KIRI: Zoom & Morphing
                        leftDetected = true;
                        const lm = marks;

                        // 1. Zoom (Jempol 4 & Kelingking 20)
                        const zoomDist = Math.hypot(lm[4].x - lm[20].x, lm[4].y - lm[20].y);
                        // Rentang Zoom dari Z=15 (dekat) ke Z=50 (jauh)
                        targetCameraZ = THREE.MathUtils.lerp(15, 50, 1.0 - zoomDist * 1.5);

                        // 2. Morphing Detection (Cek jari tegak)
                        const checkFinger = (tip, pip) => lm[tip].y < lm[pip].y; // Tegak jika tip di atas pip
                        
                        if (checkFinger(8, 6) && !checkFinger(12, 10)) {
                            morphState = 1; // SUPERNOVA! (Hanya Telunjuk)
                        } else if (checkFinger(12, 10) && !checkFinger(8, 6) && !checkFinger(16, 14)) {
                            morphState = 2; // EIFFEL (Hanya Jari Tengah)
                        } else if (checkFinger(16, 14) && !checkFinger(12, 10)) {
                            morphState = 3; // ROCKET (Hanya Jari Manis)
                        } else {
                            morphState = 0; // SATURN DEFAULT
                        }
                    }
                });

                // UPDATE UI & SHADER UNIFORMS
                let statusText = "";
                if (rightDetected) {
                    positionVariable.material.uniforms.handGravityPos.value.copy(handGravityPos);
                    statusText += "R: Gerakkan Saturnus | ";
                } else {
                    positionVariable.material.uniforms.handGravityPos.value.set(0,0,0);
                }

                if (leftDetected) {
                    positionVariable.material.uniforms.morphState.value = morphState;
                    particleMaterial.uniforms.morphState.value = morphState; // Untuk visual shader
                    statusText += `L: Zoom ${morphState == 1 ? "[SUPERNOVA]" : morphState == 2 ? "[EIFFEL]" : morphState == 3 ? "[ROCKET]" : "[NORMAL]"}`;
                } else {
                    positionVariable.material.uniforms.morphState.value = 0;
                    particleMaterial.uniforms.morphState.value = 0;
                }
                statusEl.innerText = statusText;

            } else {
                statusEl.innerText = "Tangan tidak terdeteksi";
                positionVariable.material.uniforms.handGravityPos.value.set(0,0,0);
                positionVariable.material.uniforms.morphState.value = 0;
                particleMaterial.uniforms.morphState.value = 0;
                targetCameraZ = 25; // Reset zoom
            }
        });

        const videoElement = document.getElementById('input_video');
        const cameraDevice = new Camera(videoElement, {
            onFrame: async () => { await hands.send({image: videoElement}); },
            width: 640, height: 480
        });
        cameraDevice.start();


        // --- RENDER LOOP & FISIKA ---
        const clock = new THREE.Clock();
        let currentHandX = 0, currentHandY = 0;

        function animate() {
            requestAnimationFrame(animate);
            const delta = clock.getDelta();
            const time = clock.getElapsedTime();

            // 1. Update GPGPU Uniforms
            positionVariable.material.uniforms.time.value = time;
            positionVariable.material.uniforms.delta.value = delta;

            // 2. Jalankan Komputasi GPU (Hitung Fisika & Morphing)
            gpuCompute.compute();

            // 3. Ambil Tekstur Posisi Baru dari GPU dan kirim ke Material Partikel
            particleMaterial.uniforms.texturePosition.value = gpuCompute.getCurrentRenderTarget(positionVariable).texture;
            particleMaterial.uniforms.time.value = time;

            // 4. Update Zoom Kamera (Smooth Lerp)
            camera.position.z += (targetCameraZ - camera.position.z) * 0.08;

            // 5. Sedikit rotasi otomatis grup (Normal Mode)
            if(morphState == 0) {
                mainGroup.rotation.y += 0.001;
            }

            renderer.render(scene, camera);
        }
        animate();


        // --- HELPER FUNCTIONS ---
        // Mengisi Tekstur GPGPU dengan Posisi Awal Saturnus
        function fillPositionTexture(texture) {
            const data = texture.image.data;
            for (let i = 0; i < PARTICLES; i++) {
                let x, y, z, r, type;
                
                if (i < PARTICLES * 0.4) { // 40% PLANET (BOLA)
                    const u = Math.random(), v = Math.random();
                    const theta = 2 * Math.PI * u;
                    const phi = Math.acos(2 * v - 1);
                    r = PARAMS.planetRadius * Math.pow(Math.random(), 0.7);
                    x = r * Math.sin(phi) * Math.cos(theta);
                    y = r * Math.sin(phi) * Math.sin(theta);
                    z = r * Math.cos(phi);
                    type = 0.0; // Planet
                } else { // 60% RING (CINCN)
                    const angle = Math.random() * Math.PI * 2.0;
                    r = PARAMS.ringInnerRadius + Math.pow(Math.random(), 0.6) * (PARAMS.ringOuterRadius - PARAMS.ringInnerRadius);
                    if (r > 7.5 && r < 7.9) r += (Math.random()-0.5) * 1.5; // Celah Cassini

                    x = Math.cos(angle) * r;
                    y = (Math.random() - 0.5) * 0.15; // Ketebalan cincin
                    z = Math.sin(angle) * r;
                    type = 1.0; // Ring
                }

                data[i * 4] = x; data[i * 4 + 1] = y; data[i * 4 + 2] = z;
                data[i * 4 + 3] = type; // Simpan tipe di W
            }
        }

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

    </script>
</body>
</html>
