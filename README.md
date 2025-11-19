# Music Player App

A browser-based music player that lets you play, pause, skip, shuffle, delete, and reset songs in a playlist. Built to practice basic string/array methods, objects, DOM manipulation, and accessible UI patterns.

The playlist uses free songs by Quincy Larson from the freeCodeCamp curriculum.

## Demo

The UI has two main sections:

- **Player**  
  - Album art  
  - Current song title & artist  
  - Controls: Previous, Play, Pause, Next, Shuffle  

- **Playlist**  
  - List of songs with title, artist, duration  
  - Each row has:
    - A button to play that song
    - A delete button (X) to remove the song from the playlist

When the current track ends, the player automatically moves to the next one.  
When the playlist is empty, a **“Reset Playlist”** button appears.

## Tech Stack

- **HTML** – structure for the player and playlist
- **CSS** – styling, layout, and responsive behavior
- **JavaScript** – playlist data, playback logic, and DOM updates

## Features

- Predefined playlist of 10 songs (title, artist, duration, audio URL).
- Play/pause current song.
- Skip to **next** or **previous** track.
- **Shuffle**: randomizes the order of the playlist.
- **Delete** individual songs:
  - If you delete the currently playing song, playback stops and the display is cleared.
  - When all songs are deleted, a **Reset Playlist** button appears to restore the original list.
- Highlights the current song in the playlist using `aria-current="true"`.
- Updates the Play button’s `aria-label` with the current song title for better accessibility.
- Automatically plays the next song when one ends; if there isn’t a next song, playback stops and the player resets.

## How to Run the Project

1. **Clone the repository:**

   ```bash
   git clone https://github.com/SharpSanders/music-player.git
   cd music-player
Open the app:

Option A: Double-click index.html to open it in your browser.

Option B (recommended while developing): Use the Live Server extension in VS Code and open index.html via Live Server.

You should see the freeCodeCamp player at the top and the Playlist section below.

How to Use
Play from the player controls:

Click Play to start:

If nothing has played yet, it starts the first song in the (sorted) playlist.

If a song was paused, it resumes from where it left off.

Click Pause to pause playback.

Click Next or Previous to move through the playlist.

Play from the playlist:

Click any song row in the playlist to start that song immediately.

The active song row is highlighted.

Shuffle & Delete:

Click Shuffle:

Randomizes the order of userData.songs.

Stops playback and clears the current song info.

Click the X on a song row:

Removes that song from the playlist.

If it was the current song, playback stops and the display clears.

If all songs are deleted:

A Reset Playlist button appears at the bottom.

Click it to restore the original allSongs array and re-render the playlist.

How It Works (JavaScript Overview)
All logic lives in script.js.

Data
allSongs: an array of song objects:

js
Copy code
{
  id: 0,
  title: "Scratching The Surface",
  artist: "Quincy Larson",
  duration: "4:25",
  src: "https://cdn.freecodecamp.org/..."
}
userData:

js
Copy code
let userData = {
  songs: [...allSongs],
  currentSong: null,
  songCurrentTime: 0,
};
audio: a single Audio instance used for playback.

Core Functions
playSong(id)

Finds the song by id in userData.songs.

Sets audio.src and audio.title.

If a new song is selected, starts from 0; if it’s the same song, resumes from songCurrentTime.

Updates userData.currentSong.

Highlights the current song in the playlist.

Updates the display (setPlayerDisplay) and the play button’s accessible text.

Calls audio.play().

pauseSong()

Stores audio.currentTime in userData.songCurrentTime.

Removes the .playing style from the Play button.

Calls audio.pause().

playNextSong() / playPreviousSong()

Determine the current index via getCurrentSongIndex().

Play the next or previous song in userData.songs.

shuffle()

Shuffles userData.songs in place.

Resets currentSong and songCurrentTime.

Re-renders the playlist and resets the display/accessibility text.

deleteSong(id)

If the deleted song is currently playing:

Clears currentSong and songCurrentTime.

Pauses audio and clears the display.

Filters the song out of userData.songs.

Re-renders playlist, re-applies highlight state, and adjusts accessible text.

If the playlist becomes empty, creates a Reset Playlist button.

renderSongs(array)

Generates <li> markup for each song with:

A play button wrapping title, artist, and duration.

A delete button with an SVG X icon.

Injects the markup into #playlist-songs.

Handles creation of the reset button when there are no songs.

sortSongs()

Sorts userData.songs alphabetically by title.

Called once on load before renderSongs().

Event listeners:

Buttons: play, pause, next, previous, shuffle.

audio ended event to auto-play the next song or reset if the playlist is finished.

Project Structure
text
Copy code
music-player/
├── index.html   # Player and playlist markup, SVG icons, script includes
├── styles.css   # Themed layout, player styling, responsive tweaks
└── script.js    # Song data, state management, playback controls, DOM rendering
What I Practiced
Modeling a playlist as an array of objects.

Using DOM APIs to build dynamic lists and interactive controls.

Managing UI state with a userData object.

Working with the HTMLAudioElement (new Audio()).

Using array methods (map, filter, sort) and event listeners.

Adding accessibility with aria-label and aria-current.

Future Improvements
Display playback progress and a seek bar.

Show elapsed time / remaining time.

Keyboard shortcuts for player controls.

Persist playlist state and current song in localStorage.

Allow users to add custom songs or upload local audio.

Author
Created by Trevyn Sanders.