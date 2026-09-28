# Word Games

Three co-op word games in one phone-friendly page. Each one works with 2 players or a crowd:

- **Just One:** everyone writes a one-word clue for the guesser, and matching clues cancel each other out.
  With 3 players everyone writes 2 clues. With 2, you write 3, and any clue on the word's too-obvious list is cancelled.
  Play 7, 13 or 20 cards.
- **So Clover!:** link the pairs of words on your secret four-card clover, then the others rebuild it from your clues:
  4 cards plus a decoy, each in the right spot and turned the right way. 6 points on the first try, 3 on the second.
- **Medium:** two players each play a word, then both say the word that sits between them.
  No match? The words you just said become the new pair. 3 tries, for 3, 2 or 1 point.

## Two ways to play
- **One phone:** pass it around. Secret screens stay covered until the right player taps "I'm …".
  In Medium you say your words out loud on 3-2-1, then type what you each said.
- **Rooms:** the host taps *Start a room* and shares the 4-letter code or invite link. Everyone plays on their own phone.
  Rooms are peer-to-peer (WebRTC via [PeerJS](https://peerjs.com/)), so there's no server to run.
  The host's phone runs the game, so the host keeps Word Games open. The host can play for anyone who goes offline, or remove them from the game.

A single self-contained `index.html` with no build step. One-phone mode works offline once loaded.

## Dev notes
- `?net=local` swaps PeerJS for a same-browser BroadcastChannel transport, so you can play a room across several tabs with no internet.
- `?peerhost=127.0.0.1:9000` points PeerJS at a self-hosted PeerServer (`npx peer --port 9000`).
- The word list lives at the top of the first `<script>` in `index.html`, one word per line: `Word: obvious, clues`.
  All three games draw from it. The clues after the colon are only used in two-player Just One.
- Typed words match regardless of capital letters, punctuation, "the/a" and plurals ("Oceans" = "ocean").
