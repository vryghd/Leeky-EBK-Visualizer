# Simpsons-Style p5.js Visualizer Template

This project is a high-fidelity, audio-reactive visualizer built using HTML5 Canvas and the `p5.js` library. It's designed to be easily adaptable for different songs, artists, and color schemes.

## Core Files
- `index.html`: The main logic and drawing code where everything happens.
- `Leeky EBK.m4a`: The audio file that drives the beat detection.

## How to Customize for Other Projects

### 1. Changing the Music
To swap out the song, simply replace the `Leeky EBK.m4a` file in the folder with your new audio file (MP3 or M4A). 
Open `index.html` and update line `78` where the sound is loaded:
```javascript
song = loadSound('Your_New_Song.mp3', soundLoaded, soundFailed);
```

### 2. Changing the Artist Name (Title & Tagline)
To change the "EBK" and "BY LEEKY" text that appears in the sky, navigate to the `drawText()` function near line `538`. 
```javascript
// Draw Thick Stroke for Main Title
textSize(80);
text("NEW TITLE", 0, 0); // Change "EBK" here
noStroke();
text("NEW TITLE", 0, 0);

// Draw Subtitle
textSize(30);
text("BY NEW ARTIST", 0, 60); // Change "BY LEEKY" here
noStroke();
text("BY NEW ARTIST", 0, 60);
```

### 3. Adjusting Colors
At the very top of the script (around line `30`), you'll find the global color variables. Changing these will quickly alter the vibe of the characters and background elements:
```javascript
const SIMPSONS_BLUE = '#7092BE'; // General thematic blue
const SKIN_YELLOW = '#FED90F';   // Classic Simpsons yellow for clouds/road lines
const SKIN_BROWN = '#8D5524';    // Current character skin tone
const OUTLINE = '#000000';       // The thick black stroke color
```
To change the **Gradient Sky**, update the colors in the `draw()` loop around line `98`:
```javascript
// setGradient(x, y, w, h, Top Color, Bottom Color)
setGradient(0, 0, width, height*0.66, color('#4FA6FF'), color('#87CEEB'));
```
To change the **Car Colors**, simply change the hex code passed into the `drawDetailedCarWithChar` function inside `drawCarsWithCharacters()` (around line `344`):
```javascript
// Purple Sedan (Left)
drawDetailedCarWithChar(width * 0.1, roadY + 40 + carBounce, '#9b59b6', false);

// Green Sedan (Right)
drawDetailedCarWithChar(width * 0.6, roadY + 60 + carBounce, '#27ae60', true);
```

### 4. Audio Reactivity (Beat Thresholds)
The shooting, screen shakes, and bullets are all tied to the *amplitude* (volume) of the audio track. To make these effects trigger more easily (or less often) based on a different song, adjust the threshold in the `draw()` loop near line `112`:
```javascript
// 0.3 is the required amplitude. Lower logic = triggers on quieter sounds.
if (level > 0.3 && flashTimer <= 0) { 
  isFiring = true;
  flashTimer = 5; 
}
```

## Running the Application
Security policies in modern web browsers actively prevent autoplaying local audio files from double-clicking an `.html` file.
To view and run the visualizer properly, you must run it through a local server.

**Quick Mac Terminal Command:**
```bash
cd "path/to/project/folder"
python3 -m http.server 8000
```
Then open `http://localhost:8000/index.html` in Safari or Chrome.

**Note:** Always remember to click anywhere on the canvas right when it loads to "resume" the Web Audio Context and ensure the music loop starts.
