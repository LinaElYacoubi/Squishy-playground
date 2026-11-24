Squishy's Playground

A touch-free 3D game for the INNOVA holographic display at the University of Ottawa.

Squishy is a pink jelly creature. Visitors control it with one hand in the air in front of a webcam: move to aim, pinch to grab, open to let go.

Built with TypeScript, Three.js, MediaPipe Hand Landmarker and Vite. No backend, no 3D model files, no cloud processing.

Features

Free Play

Grab and stretch: pinch Squishy and it follows your hand like jelly.
Throw: let go during a quick flick and it bounces around the screen.
Feed: drag a fruit from the tray to Squishy's mouth.
Pet: wave an open hand slowly above its head.
Mini me and Merge Magic: split Squishy into three minis, then merge two into a Star, Ocean or Galaxy Jelly.
Two players: two hands (or two visitors) can play at once.
Moods: Squishy gets hungry, sleepy, picks a favourite snack and makes friends.

Mini-games (pinch the "Play with me!" bubble)

Game	Goal
Squishy Says	Repeat the bubble sequence Squishy shows you
Snack Surprise	Feed Squishy the snack it asks for
Bubble Bounce	Toss Squishy through floating bubbles

Also: English/French toggle, optional sound effects, and automatic reset after 30 seconds without a visitor.

Run it

Requires Node.js 22.12+, Chrome or Edge, and a webcam.

bash
npm install     # install packages and download the hand model
npm run dev     # start at http://localhost:5173
npm run build   # production build in dist/
npm test        # run the unit tests

The camera only works on localhost or https://, not when opening index.html directly.

Setup at the display
Press O to open the operator panel, then Enable camera.
Place the webcam facing visitors at chest height, 1–2.5 m away, with light in front of them.
Choose a display mode: Hologram capsule (4K portrait), Desktop preview or Black background.
Adjust Safe margins to fit the screen, press Fullscreen, and close the panel.

Mouse test mode in the panel lets you test everything without a webcam (click = pinch).

How it works
Hand tracking: MediaPipe runs in a Web Worker so the 3D scene stays smooth.
Pinch detection: measures the thumb-to-index distance, with separate grab and release thresholds so it doesn't flicker.
Cursor smoothing: a One Euro filter removes jitter without adding lag.
Throwing: speed is estimated from the last moments of hand movement before release.

Most settings (sizes, speeds, timings, colours) are in src/config.ts.

Privacy

Video is processed only in the browser and is never recorded or uploaded. A test (tests/privacy.test.ts) fails if any network or recording code is added.

Testing

161 unit tests (Vitest) cover gestures, throwing, feeding, merging, mini-games, two players, language and privacy, using simulated input.

Still to test on real hardware: tuning with real visitors' hands, and performance and glow on the holographic capsule.

Project structure
src/
  input/      hand tracking, pinch detection, cursor smoothing
  game/       gameplay, physics, throwing, mini-games
  creature/   Squishy and food (3D shapes, faces, animation)
  scene/      renderer, lighting, effects
  ui/         visitor text (EN/FR) and operator panel
  audio/      sound effects
  config.ts   all tuning values
tests/        unit tests
