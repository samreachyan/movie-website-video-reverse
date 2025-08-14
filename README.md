# Movie Website to Video reverse

## How it works

The website has stream video from the CDN

You can see:

- Ne Zha II: https://cdn.anajakhd.com/file/anajakvideos/NeZha2/master.m3u8

- CreationGodII: https://cdn.anajakhd.com/file/anajakvideos/CreationoftheGodsII/master.m3u8

- Hit Man 2: https://cdn.anajakhd.com/file/anajakvideos/Hitman2/master.m3u8 

- The Monkey Kind 3: https://cdn.anajakhd.com/file/anajakvideos/TheMonkeyKing3/master.m3u8

- Cosmoball : https://cdn.anajakhd.com/file/anajakvideos/Cosmoball/master.m3u8

- How to train your dragon: https://cdn.anajakhd.com/file/anajakvideos/HowToTrainYourDragon/master.m3u8

- 28 Years later: https://cdn.anajakhd.com/file/anajakvideos/28YearsLater/master.m3u8

- Sakra: https://cdn.anajakhd.com/file/anajakvideos/Sakra/master.m3u8

- The Ghost Station: https://cdn.anajakhd.com/file/anajakvideos/TheGhostStation/master.m3u8

- KarateKidLegends: https://cdn.anajakhd.com/file/anajakvideos/KarateKidLegends/master.m3u8

- Waktu Maghrib: https://cdn.anajakhd.com/file/anajakvideos/WaktuMaghrib/master.m3u8

- I am what I am : https://cdn.anajakhd.com/file/anajakvideos/IAmWhatIAm/master.m3u8

- Kampung Keramat: https://cdn.anajakhd.com/file/anajakvideos/KampungKeramat/master.m3u8

- The Sonic The Hedgehog: https://cdn.anajakhd.com/file/anajakvideos/SonicTheHedgehog3//master.m3u8

- Ballerina: https://cdn.anajakhd.com/file/anajakvideos/Ballerina/master.m3u8

- A Working Man: https://cdn.anajakhd.com/file/anajakvideos/AWorkingMan/master.m3u8

- Munafik: https://cdn.anajakhd.com/file/anajakvideos/Munafik/master.m3u8

- Munafik-2: https://cdn.anajakhd.com/file/anajakvideos/Munafik2/master.m3u8

- Zombie Hunter: https://cdn.anajakhd.com/file/anajakvideos/ZombieHunter/master.m3u8

- Vina Before 7 Days: https://cdn.anajakhd.com/file/anajakvideos/VinaBefore7Days/master.m3u8

- Haunted Road 2: https://cdn.anajakhd.com/file/anajakvideos/HauntedRoad2/master.m3u8

- Red Cliff 2: https://cdn.anajakhd.com/file/anajakvideos/RedCliff2/master.m3u8

- ShangHai-Noon: https://cdn.anajakhd.com/file/anajakvideos/ShanghaiNoon/master.m3u8


## Put my code on console log

After go to the website, you can just click on the console log and put the code below into the console:

```javascript
(function () {
  // Step 1: Inject CSS into <head>
  const style = document.createElement('style');
  style.textContent = `
    body {
      margin: 0;
      padding: 20px;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background-color: #f0f0f0;
    }
    .video-container {
      max-width: 800px;
      width: 100%;
    }
    video {
      width: 100%;
      height: auto;
      background-color: #000;
    }
  `;
  document.head.appendChild(style);

  // Step 2: Create video container and video element
  const videoContainer = document.createElement('div');
  videoContainer.className = 'video-container';
  videoContainer.innerHTML = `
    <video id="player" controls autoplay muted>
      <source src="https://cdn.anajakhd.com/file/anajakvideos/Hitman2/master.m3u8" type="application/x-mpegURL">
      Your browser does not support the video tag.
    </video>
  `;
  document.body.innerHTML = ''; // Clear existing body content (optional, remove if you want to append)
  document.body.appendChild(videoContainer);

  // Step 3: Load HLS.js script dynamically
  const hlsScript = document.createElement('script');
  hlsScript.src = 'https://cdn.jsdelivr.net/npm/hls.js@latest';
  hlsScript.onload = () => {
    // Step 4: Initialize video player after HLS.js loads
    const video = document.getElementById('player');
    const hlsUrl = 'https://cdn.anajakhd.com/file/anajakvideos/Hitman2/master.m3u8';

    if (window.Hls && Hls.isSupported()) {
      const hls = new Hls();
      hls.loadSource(hlsUrl);
      hls.attachMedia(video);
      hls.on(Hls.Events.MANIFEST_PARSED, () => {
        video.play().catch(error => console.error('Auto-play failed:', error));
      });
      hls.on(Hls.Events.ERROR, (event, data) => {
        console.error('HLS error:', data);
      });
    } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
      video.src = hlsUrl;
      video.addEventListener('loadedmetadata', () => {
        video.play().catch(error => console.error('Auto-play failed:', error));
      });
    } else {
      console.error('HLS is not supported in this browser.');
    }
  };
  hlsScript.onerror = () => console.error('Failed to load HLS.js');
  document.head.appendChild(hlsScript);
})();
```

If you can to change the movie, just change 2 variables:

- videoContainer.innerHTML 
- hlsUrl 
