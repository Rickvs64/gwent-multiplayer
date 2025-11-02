# About
Play Gwent (the classic Witcher 3 version) in the browser against another human opponent.
Full complete multiplayer, every card and ability functional (let me know if not).
Tweaked variant of Leo-Felde's multiplayer Gwent project (https://github.com/Leo-Felde/gwent-multiplayer) with the following changes:
* Fixed some issues where both clients would desynchronize.
  * Overall replication of "which card did the client draw/select/revive/etc" is now always done based on filename instead of hand/deck/graveyard index, which seemed to be unreliable.
  * Emhyr's leader card that prevents players from picking which card to revive upon playing a Medic now always revives the strongest card; previously it would choose a random card that differs per client.
  * Monster faction ability now keeps the strongest card on the board after every round; previously it would choose a random card that differs per client.
  * Skellige faction ability now revives the two strongest cards at the start of round 3; previously it would choose a random card that differs per client.
  * Eredin's leader card that discards two cards and selects one from deck now properly refreshes hand carousel between steps and replicates selected cards; previously it would fail to inform the opponent of both actions correctly.
* Changed `gwent.js` and `server.js` structure to specifically support deployment on online platforms such as render.com.
  * Local play still works, see below.
* Some more minor things my dumb ass forgot to annotate in code.
 
# How to use (A or B)
## A. Online demo
I deployed the latest commit on https://gwent-render.onrender.com/.
It's just hosted on a free plan so can't vouch for the URL remaining online since the time of writing but maybe it's still available.
Downloading the project is faster and more reliable.
## B. Download and play
* Both players:
  * Download the project.
  * Change `gwent.js` to point to the host player's IP.
    * For example, `const socket = new WebSocket('ws://192.168.178.20:8080');`   (`ws`, _not_ `wss` in this case)
  * Open index.html in the browser.
* Host player (someone needs to run the server):
  * Install Node.js.
  * Opan a command prompt window in the project root folder.
  * Run `npm install` to install prerequisite packages.
  * Run `node server.js` to start the server.
  * Keep server running while playing the game, duh.
 
# Credits
Full credit and thanks go to CD Projekt Red for creating The Witcher 3, [asundr for the base browser recreation of Gwent](https://github.com/asundr/gwent-classic) and [Leo-Felde for the base multiplayer fork](https://github.com/Leo-Felde/gwent-multiplayer). I only added some fixes.
