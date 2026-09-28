# Ant Stomp

A two-player picnic game played with one finger each. A barrier splits the screen in two. Each player defends their own cake against a stream of ants and squashes them with their index finger. Highest score wins.

Your hands are tracked in the browser with [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker). Your video never leaves your device.

## Deploy on GitHub Pages

1. Create a new repository on GitHub.
2. Upload `index.html`, this `README.md` **and the `ants` folder** (it holds the ant faces) to the repository root.
3. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, pick `main` and `/ (root)`, then **Save**.
4. After a minute your game is live at `https://<your-username>.github.io/<repo-name>/`.

Camera access only works on `https://` pages (GitHub Pages qualifies) or `http://localhost`. Opening `index.html` straight from disk won't work for the camera; run `python3 -m http.server` instead.

## How to play

- Sit or stand side by side, about an arm's length from the camera, and hold your hands up. **Player 1 plays the left side of the screen (blue), Player 2 the right side (gold).** A hazard-tape barrier runs down the middle.
- **One finger per player.** Your crusher is the tip of your **index finger**: point it at an ant to squash it. It shows as a coloured circle with a white dot. Thumbs, other fingers, palms and everything else do nothing.
- **One hand per player.** If you hold up two hands, only one is active (the other is drawn faintly). The tracker keeps using the hand you were already playing with, or picks the bigger hand at the start.
- **The barrier is solid.** A hand belongs to the side its wrist is on, and its index fingertip only works on that side. If it reaches over or onto the barrier, the circle turns grey and dashed and does nothing. Ants can't cross either.
- Both sides get the same ants at the same time, so the match is fair. Normal ants score 10, fast red ants 20, and big black ants 50 (they take three hits). Crushing ants in quick succession builds a combo multiplier up to x5.
- Ants that reach your cake eat a slice. The round ends when the 90-second clock runs out, or as soon as either cake is gone.
- **The higher score wins.** If it's level, the player with more cake left wins. If that's level too, it's a tie. The winner is revealed after the scores count up.

**No camera?** Choose *Play with mouse or touch*. Player 1 taps the left side and Player 2 the right. Multi-touch works, so two people can tap at once on a tablet.

**On a phone held upright** the touch game splits the screen top and bottom instead: Player 1 plays the top half and Player 2 the bottom, so each gets a usable area. Turn the phone sideways to get the left/right split back. Camera play always splits left/right, since the players stand side by side.

**Solo practice** removes the barrier and the clock (still one finger). One cake, five slices, and a saved best score.

## The ant heads

Pick the heads on the menu under **Ant heads**:

- **Artwork (default)**: each ant's head is one of the six artworks in `ants/` (`art-1.jpg` to `art-6.jpg`), shown as-is in a round frame that stays upright while the little ant body scuttles behind it. Normal ants use `art-1` and `art-2`, fast ants use `art-3` and `art-4`, and big ants (crowned, three hits) use `art-5` and `art-6`.
- **Goofy pixels**: the same six faces reduced to 9x9 or 11x11 pixel mosaics (`pixel-1.png` to `pixel-6.png`) with googly eyes, clown noses, moustaches, tongues and party hats added.
- **Classic**: plain googly-eyed ants with bow ties and shades. This is also the automatic fallback if the images can't load.

A squashed ant leaves a flattened version of its head on the blanket, and its ghost floats up wearing a halo.

**To use your own images:** save them in `ants/` (square-ish, roughly 300 px, with the face centred) and edit the `FACE_SETS` lists at the top of the script. Faces are cropped to a circle. Head size is `FACE_R`.

**Rights:** the bundled artworks are other artists' work (two still carry visible signatures) and depict real people. Get permission before publishing the game publicly, or swap in your own drawings, and only use faces of people who would enjoy being squashed in a silly game.

## The silly bits

- **The ants have personalities.** They wear shades, bow ties and moustaches (fast ants get racing goggles, big ants wear crowns), have googly eyes, and chat as they march ("Are we there yet?", "I brought snacks", "I AM CHONK").
- **They panic.** Bring your finger near an ant and its eyes go wide, its legs go faster, and it yells things like "Not the finger!" and "Abort! ABORT!".
- **Last words.** Squashed ants get a final line, then float up to heaven with a halo and wings.
- **The cake has feelings.** It starts happy, gets worried as slices disappear, and screams when it's nearly gone. It also yelps when bitten.
- **An over-excited announcer** calls out combos (TRIPLE SQUISH!, ANT-POCALYPSE!), lead changes, speedy ants, chonkers and PANIC TIME in the last 10 seconds.
- **Silly sounds:** squeaks, bonks and nom-nom chomps (there's a Sound button).
- **Results with attitude:** every player earns a title (from *Ant Whisperer* to *Grand Ant-ihilator*) and the winner gets a random verdict.

## Notes

- Good, even lighting and a plain background make hand tracking much more reliable.
- Point clearly with your index finger, with the hand in view of the camera. Keep your hands apart from the other player's.
- If one player's hand disappears for a few seconds, a hint appears telling them to hold it up.
- **First load** downloads the hand model (a few MB) and runtime, so the first start takes a few seconds.
- **Tuning.** Crusher size is `TIP_R`, barrier width is `BARRIER`, round length is `MATCH_SECONDS`, and ant stats are in `TYPES`, all near the top of the script.
