🎽 Sahayak AI — Live Monitoring Demo

A browser-based simulation of Sahayak AI, a wearable clip-on safety assistant that continuously watches the user's surroundings and warns them about hazards through color-coded status, voice alerts, and vibration. No pointing or holding the phone is needed: the camera runs continuously and the user is alerted hands-free.

This repository contains the software demo (Phase 1). It uses the device camera of your phone or laptop to simulate what the wearable hardware will do in Phase 2.

✨ Features
Continuous live monitoring using the device camera (rear camera preferred on phones)
Three-level alert system
🟢 SAFE: path is clear
🟠 CAUTION: low light, nearby person or obstacle
🔴 DANGER: fire-like colors or an immediate hazard
Voice alerts using the Web Speech API (text-to-speech) for CAUTION and DANGER
Haptic feedback using the Vibration API, with different patterns for CAUTION and DANGER
Live alert log with timestamps and color-coded badges
Demo buttons to instantly simulate DANGER and CAUTION scenarios, useful when presenting without a real hazard
Zero dependencies: a single index.html file with plain HTML, CSS and JavaScript
🧠 How the detection works

Every 2.5 seconds the app grabs a frame from the live video, downsamples it to 64×48 pixels on a hidden canvas, and computes:

Average brightness across all pixels
Red-channel dominance: average red minus the average of green and blue

These values decide the alert level:

Condition	Alert	Message
Red dominance > 25 and brightness > 60	🔴 DANGER	Fire-like colors detected ahead
Brightness < 40	🟠 CAUTION	Low light and obstacle ahead
Otherwise	🟢 SAFE (occasionally 🟠 CAUTION)	Path is clear / person nearby

⚠️ Note: This is a lightweight, explainable heuristic built for a prototype. The "person nearby" caution is a placeholder that appears randomly to show alert variety. It does not use real object detection yet. The detection function is designed to be replaced by a trained vision model or a vision/LLM API (see Roadmap).

🚀 Getting Started
Run locally
Clone the repository
bash
   git clone 
   cd sahayak-ai
Serve the file over localhost (browsers only allow camera access on localhost or HTTPS)
bash
   # Python
   python -m http.server 8000

   # or Node.js
   npx serve .
Open http://localhost:8000 in your browser
Click ▶ Start Monitoring and allow camera access
Try it on your phone

Host the page on GitHub Pages, Netlify or Vercel (all provide HTTPS), then open the link on your phone. The rear camera is used by default.

🎮 Usage
Button	What it does
▶ Start Monitoring	Starts the camera and begins analysing frames every 2.5 s
■ Stop	Stops the camera and the analysis loop
🔥 Simulate Danger	Triggers a demo DANGER alert with voice and vibration
⚠️ Simulate Caution	Triggers a demo CAUTION alert with voice and vibration
🛠️ Tech Stack
HTML5, CSS3, Vanilla JavaScript
MediaDevices.getUserMedia for camera access
Canvas API for frame sampling and pixel analysis
Web Speech API (speechSynthesis) for voice alerts
Vibration API for haptic feedback
🌐 Browser Support
Feature	Support
Camera + analysis	All modern browsers (HTTPS or localhost)
Voice alerts	Chrome, Edge, Safari, Firefox
Vibration	Mostly Android Chrome; not supported on iOS Safari
🗺️ Roadmap
 Phase 1: Browser demo with continuous monitoring, voice and vibration alerts
 Phase 2: Hardware version on an ESP32-CAM pendant clipped to a collar or lanyard, streaming to the phone over Wi-Fi
 Replace the color heuristic with a real object detection model (for example TensorFlow.js or a vision API)
 Distance estimation and direction guidance (left / right / ahead)
 Multilingual voice alerts (including Hindi and Gujarati)
 Offline mode and a caregiver alert option
📁 Project Structure
.
├── index.html   # Entire app: UI, styles and detection logic
└── README.md
🤝 Contributing

Suggestions and pull requests are welcome. Please open an issue first to discuss major changes.

📄 License

This project is licensed under the MIT License. Add a LICENSE file to your repository if you choose this option.

👤 Author

Kajal Baraiya GitHub: @kajalbaraiya
