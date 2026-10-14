# JavaScript Game Development Cheatsheet (Searchable) (11\_18\_2025 7：37：59 AM)

Jason Davis — https://codepen.io/Jason-Davis-the-vuer

This page contains a consolidated cheatsheet for JavaScript game development: fundamentals, canvas games, text-based games, idle/incremental mechanics, puzzle games, and blockchain integration examples. Code examples are included as-is.

***

### Introduction to JavaScript Game Development

JavaScript has become a powerful platform for game development, offering the ability to create engaging games that run in web browsers without plugins. This cheatsheet provides a comprehensive guide to developing different types of games with JavaScript, from fast-paced canvas games to text adventures and idle games, with details on blockchain integration for each type.

Whether you're a beginner looking to create your first game or an experienced developer exploring new game genres or blockchain integration, this resource offers code examples, design patterns, and best practices to help you build successful JavaScript games.

***

### Game Development Fundamentals

#### Game Loop

The heart of any game is the game loop, which updates the game state and renders the changes:

```javascript
// Basic game loop
function gameLoop() {
  update(); // Update game state
  render(); // Render the changes
  requestAnimationFrame(gameLoop); // Schedule next frame
}

// Start the game
requestAnimationFrame(gameLoop);
```

#### Input Handling

Capturing user input is essential for interactive games:

```javascript
// Track key states
const keys = {};

// Set up event listeners
window.addEventListener('keydown', (e) => {
  keys[e.key] = true;
});
window.addEventListener('keyup', (e) => {
  keys[e.key] = false;
});

// Check key state in update function
function update() {
  if (keys['ArrowRight']) {
    player.x += player.speed;
  }
}
```

#### Time Management

For smooth animations and gameplay independent of frame rate:

```javascript
let lastTime = 0;

function gameLoop(timestamp) {
  // Calculate delta time in seconds
  const deltaTime = (timestamp - lastTime) / 1000;
  lastTime = timestamp;

  update(deltaTime); // Pass delta time to update
  render();

  requestAnimationFrame(gameLoop);
}

function update(dt) {
  // Move based on time, not frames
  player.x += player.speed * dt;
}
```

***

### Canvas Games

Canvas games use the HTML5 Canvas API to create visually rich, action-packed games. The Canvas provides a direct way to manipulate pixels, making it ideal for 2D games like platformers, shooters, and arcade-style games.

{% tabs %}
{% tab title="Canvas Basics" %}
#### Canvas Setup and Drawing

Setting up a canvas and drawing basic shapes:

```javascript
// Get canvas and context
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

// Set canvas size
canvas.width = 800;
canvas.height = 600;

// Draw rectangle
ctx.fillStyle = 'red';
ctx.fillRect(50, 50, 100, 100);

// Draw circle
ctx.beginPath();
ctx.fillStyle = 'blue';
ctx.arc(300, 100, 50, 0, Math.PI * 2);
ctx.fill();

// Draw text
ctx.font = '24px Arial';
ctx.fillStyle = 'black';
ctx.fillText('Game Title', 400, 100);
```

#### Sprites and Image Loading

Loading and rendering sprite images:

```javascript
// Load sprite image
const playerSprite = new Image();
playerSprite.src = 'player.png';
playerSprite.onload = () => {
  // Image is ready to use
};

// Draw sprite
function drawPlayer(x, y) {
  ctx.drawImage(playerSprite, x, y, 64, 64);
}

// Sprite animation with sprite sheet
function drawAnimatedSprite(x, y, frameX, frameY) {
  const spriteWidth = 64;
  const spriteHeight = 64;
  ctx.drawImage(
    playerSprite,
    frameX * spriteWidth, frameY * spriteHeight, // Source position
    spriteWidth, spriteHeight,                   // Source dimensions
    x, y,                                         // Destination position
    spriteWidth, spriteHeight                    // Destination dimensions
  );
}
```
{% endtab %}

{% tab title="Animation Loops" %}
#### Animation Fundamentals

Creating smooth animations with requestAnimationFrame:

```javascript
// Game state
const game = {
  player: {
    x: 100,
    y: 100,
    width: 50,
    height: 50,
    speed: 200, // pixels per second
    color: 'blue'
  }
};
let lastTime = 0;

// Main game loop
function gameLoop(timestamp) {
  // Calculate delta time
  const deltaTime = (timestamp - lastTime) / 1000; // convert to seconds
  lastTime = timestamp;

  // Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Update player position
  if (keys['ArrowRight']) { game.player.x += game.player.speed * deltaTime; }
  if (keys['ArrowLeft']) { game.player.x -= game.player.speed * deltaTime; }
  if (keys['ArrowUp']) { game.player.y -= game.player.speed * deltaTime; }
  if (keys['ArrowDown']) { game.player.y += game.player.speed * deltaTime; }

  // Keep player within bounds
  game.player.x = Math.max(0, Math.min(canvas.width - game.player.width, game.player.x));
  game.player.y = Math.max(0, Math.min(canvas.height - game.player.height, game.player.y));

  // Draw player
  ctx.fillStyle = game.player.color;
  ctx.fillRect(game.player.x, game.player.y, game.player.width, game.player.height);

  // Schedule next frame
  requestAnimationFrame(gameLoop);
}
```

#### Particle Systems

Creating dynamic particle effects:

```javascript
// Particle class
class Particle {
  constructor(x, y) {
    this.x = x; this.y = y;
    this.size = Math.random() * 5 + 2;
    this.speedX = Math.random() * 3 - 1.5;
    this.speedY = Math.random() * 3 - 1.5;
    this.color = 'rgba(255,255,255,0.7)';
    this.life = 1.0; // Starting opacity
    this.decay = Math.random() * 0.02 + 0.005;
  }
  update() {
    this.x += this.speedX; this.y += this.speedY; this.life -= this.decay;
  }
  draw(ctx) {
    ctx.fillStyle = this.color.replace('0.7', this.life);
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fill();
  }
}
// Manage particles
const particles = [];
function createExplosion(x, y, amount = 20) {
  for (let i = 0; i < amount; i++) particles.push(new Particle(x, y));
}
function updateParticles() {
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].draw(ctx);
    if (particles[i].life <= 0) particles.splice(i, 1);
  }
}
```
{% endtab %}

{% tab title="Collision Detection" %}
#### Collision Detection Techniques

Rectangle Collision (AABB):

```javascript
function checkRectCollision(rect1, rect2) {
  return (
    rect1.x < rect2.x + rect2.width &&
    rect1.x + rect1.width > rect2.x &&
    rect1.y < rect2.y + rect2.height &&
    rect1.y + rect1.height > rect2.y
  );
}
```

Circle Collision:

```javascript
function checkCircleCollision(circle1, circle2) {
  const dx = circle1.x - circle2.x;
  const dy = circle1.y - circle2.y;
  const distance = Math.sqrt(dx * dx + dy * dy);
  return distance < circle1.radius + circle2.radius;
}
```

Tilemap Collision (point-based check):

```javascript
const tileMap = [
  [1,1,1,1,1,1,1,1],
  [1,0,0,0,0,0,0,1],
  [1,0,1,1,0,1,0,1],
  [1,0,0,0,0,1,0,1],
  [1,1,1,1,1,1,1,1]
];
const TILE_SIZE = 32;

function isSolidTile(x, y) {
  const tileX = Math.floor(x / TILE_SIZE);
  const tileY = Math.floor(y / TILE_SIZE);
  if (tileX < 0 || tileX >= tileMap[0].length || tileY < 0 || tileY >= tileMap.length) {
    return true; // Out of bounds is solid
  }
  return tileMap[tileY][tileX] === 1;
}

function handlePlayerTileCollision(player) {
  const corners = [
    { x: player.x, y: player.y },
    { x: player.x + player.width, y: player.y },
    { x: player.x, y: player.y + player.height },
    { x: player.x + player.width, y: player.y + player.height }
  ];
  for (const corner of corners) {
    if (isSolidTile(corner.x, corner.y)) return true;
  }
  return false;
}
```
{% endtab %}

{% tab title="Blockchain Integration" %}
#### Blockchain Integration for Canvas Games

In-game assets as NFTs and interacting with smart contracts:

```javascript
// Connect to blockchain wallet (e.g., MetaMask)
async function connectWallet() {
  if (window.ethereum) {
    try {
      const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
      return accounts[0]; // connected address
    } catch (error) {
      console.error('User rejected connection', error);
    }
  } else {
    console.error('No web3 provider detected');
  }
}

// Load player NFTs (simplified, requires web3/ethers setup)
async function loadPlayerNFTs(walletAddress, contractAddress) {
  const contract = new web3.eth.Contract(nftABI, contractAddress);
  const tokenIds = await contract.methods.tokensOfOwner(walletAddress).call();
  const playerNFTs = await Promise.all(tokenIds.map(async (tokenId) => {
    const tokenURI = await contract.methods.tokenURI(tokenId).call();
    const response = await fetch(tokenURI);
    const metadata = await response.json();
    return {
      id: tokenId,
      name: metadata.name,
      image: metadata.image,
      attributes: metadata.attributes,
      speed: getAttributeValue(metadata.attributes, 'speed'),
      strength: getAttributeValue(metadata.attributes, 'strength')
    };
  }));
  return playerNFTs;
}

function getAttributeValue(attributes, traitType) {
  const attribute = attributes.find(attr => attr.trait_type === traitType);
  return attribute ? attribute.value : 0;
}
```

Saving game state on-chain (example pattern):

```javascript
async function saveHighScore(score, level) {
  if (!window.ethereum || !playerAddress) { console.error('No wallet connection'); return false; }
  try {
    const gameContract = new web3.eth.Contract(gameABI, gameContractAddress);
    const gasEstimate = await gameContract.methods.submitScore(score, level).estimateGas({ from: playerAddress });
    const result = await gameContract.methods.submitScore(score, level).send({ from: playerAddress, gas: Math.floor(gasEstimate * 1.2) });
    console.log('Score saved to blockchain', result);
    return true;
  } catch (error) {
    console.error('Error saving score:', error);
    return false;
  }
}

async function getLeaderboard() {
  const gameContract = new web3.eth.Contract(gameABI, gameContractAddress);
  const topScores = await gameContract.methods.getTopScores(10).call();
  return topScores.map(entry => ({
    address: entry.player,
    score: parseInt(entry.score),
    level: parseInt(entry.level),
    timestamp: new Date(parseInt(entry.timestamp) * 1000)
  }));
}
```
{% endtab %}
{% endtabs %}

***

### Text-Based Games

Text-based games focus on narrative and decision-making rather than graphics. They range from simple choice-driven stories to complex interactive fiction with inventory and state systems.

{% tabs %}
{% tab title="Game Structure" %}
#### Structuring a Text-Based Game

Scene-based architecture:

```javascript
// Scene-based game structure
const game = {
  currentScene: 'start',
  player: {
    name: '',
    inventory: [],
    stats: { health: 100, gold: 10 },
    flags: {}
  },
  scenes: {
    'start': {
      text: 'You wake up in a dark room. There\'s a door to the NORTH and a window to the EAST.',
      choices: [
        { text: 'Go NORTH', nextScene: 'hallway' },
        { text: 'Look out the WINDOW', nextScene: 'window' },
        { text: 'Search the ROOM', nextScene: 'search_room' }
      ]
    },
    'hallway': {
      text: 'You enter a long hallway. There are doors on both sides.',
      choices: [
        { text: 'Try the first door', nextScene: 'first_door' },
        { text: 'Continue down the hallway', nextScene: 'end_of_hallway' },
        { text: 'Go back to the room', nextScene: 'start' }
      ]
    }
    // More scenes...
  },
  renderScene() {
    const scene = this.scenes[this.currentScene];
    console.log(scene.text);
    scene.choices.forEach((choice, index) => console.log(`${index + 1}: ${choice.text}`));
  },
  makeChoice(choiceIndex) {
    const scene = this.scenes[this.currentScene];
    const choice = scene.choices[choiceIndex];
    if (choice) {
      this.currentScene = choice.nextScene;
      this.renderScene();
    }
  }
};
```

Advanced conditional choices:

```javascript
const scene = {
  text: 'You approach the castle gate. Two guards block your path.',
  getChoices() {
    const choices = [{ text: 'Turn back and find another way', nextScene: 'forest_path' }];

    if (player.inventory.includes('royal_seal')) {
      choices.push({
        text: 'Show the royal seal',
        nextScene: 'castle_entry',
        onSelect: () => { game.addToLog('The guards bow and let you pass.'); }
      });
    }
    if (player.stats.charisma >= 7) {
      choices.push({
        text: 'Try to talk your way in [Charisma]',
        nextScene: 'castle_entry',
        onSelect: () => { game.addToLog('Your silver tongue impresses the guards.'); player.stats.reputation += 1; }
      });
    }
    return choices;
  }
};
```
{% endtab %}

{% tab title="State Management" %}
#### Managing Game State

Example GameState class: inventory, flags, time progression, save/load:

```javascript
class GameState {
  constructor() {
    this.player = { name: 'Hero', inventory: [], stats: { health: 100, strength: 5, intelligence: 5 } };
    this.world = {
      currentLocation: 'village',
      time: { day: 1, period: 'morning' },
      flags: {},
      characters: { merchant: { attitude: 'neutral', metPlayer: false } }
    };
    this.quests = { 'find_artifact': { status: 'not_started', progress: 0 } };
  }

  addItem(item) { this.player.inventory.push(item); return `${item.name} added to inventory`; }

  removeItem(itemId) {
    const index = this.player.inventory.findIndex(item => item.id === itemId);
    if (index !== -1) { const item = this.player.inventory[index]; this.player.inventory.splice(index, 1); return `${item.name} removed from inventory`; }
    return 'Item not found';
  }

  hasItem(itemId) { return this.player.inventory.some(item => item.id === itemId); }

  setFlag(flagName, value = true) { this.world.flags[flagName] = value; }
  checkFlag(flagName) { return this.world.flags[flagName] || false; }

  advanceTime() {
    const periods = ['morning','afternoon','evening','night'];
    let currentIndex = periods.indexOf(this.world.time.period);
    currentIndex = (currentIndex + 1) % periods.length;
    this.world.time.period = periods[currentIndex];
    if (currentIndex === 0) this.world.time.day += 1;
    return `Time is now ${this.world.time.period} of day ${this.world.time.day}`;
  }

  save() {
    try {
      const data = JSON.stringify({ player: this.player, world: this.world, quests: this.quests });
      localStorage.setItem('textGameSave', data);
      return true;
    } catch (e) { console.error('Error saving game:', e); return false; }
  }

  load() {
    try {
      const data = localStorage.getItem('textGameSave');
      if (data) { const parsed = JSON.parse(data); this.player = parsed.player; this.world = parsed.world; this.quests = parsed.quests; return true; }
      return false;
    } catch (e) { console.error('Error loading game:', e); return false; }
  }
}
```
{% endtab %}

{% tab title="UI Design" %}
#### UI Design for Text Games

Controller pattern for story text, choices, inventory, stats, save/load and accessibility:

```javascript
class TextGameUI {
  constructor(gameContainer, game) {
    this.container = document.getElementById(gameContainer);
    this.game = game;
    this.elements = {
      storyText: document.createElement('div'),
      choicesContainer: document.createElement('div'),
      inventoryButton: document.createElement('button'),
      inventoryPanel: document.createElement('div'),
      statsButton: document.createElement('button'),
      statsPanel: document.createElement('div'),
      saveButton: document.createElement('button'),
      loadButton: document.createElement('button')
    };
    this.setupUI();
    this.bindEvents();
  }

  setupUI() { /* builds DOM elements, styling omitted here */ }
  bindEvents() {
    this.elements.inventoryButton.addEventListener('click', () => { this.togglePanel(this.elements.inventoryPanel); this.updateInventory(); });
    this.elements.statsButton.addEventListener('click', () => { this.togglePanel(this.elements.statsPanel); this.updateStats(); });
    this.elements.saveButton.addEventListener('click', () => { this.game.save(); this.showNotification('Game saved!'); });
    this.elements.loadButton.addEventListener('click', () => { if (this.game.load()) { this.update(); this.showNotification('Game loaded!'); } else { this.showNotification('No saved game found.'); } });
  }

  updateStory(text) { this.elements.storyText.innerHTML = `<p>${text}</p>`; }
  updateChoices(choices) { /* renders choice buttons and binds click handlers */ }
  updateInventory() { /* renders inventory */ }
  updateStats() { /* renders stats */ }
  showNotification(message, duration = 3000) { /* temporary notification */ }

  update() {
    const currentScene = this.game.scenes[this.game.currentScene];
    this.updateStory(currentScene.text);
    this.updateChoices(currentScene.choices);
  }
}
```

Accessibility additions (ARIA, keyboard shortcuts, high contrast, text size controls) are shown in the original examples and follow the same pattern.
{% endtab %}

{% tab title="Blockchain Integration" %}
#### Blockchain Integration for Text-Based Games

Recording significant choices on-chain, using smart contracts for persistent choices and game items:

```javascript
class BlockchainStoryGame extends TextGameBase {
  constructor(contractAddress) {
    super();
    this.contractAddress = contractAddress;
    this.playerAddress = null;
    this.significantChoices = [];
  }

  async connectWallet() {
    if (window.ethereum) {
      try {
        const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
        this.playerAddress = accounts[0];
        await this.loadPlayerChoices();
        return true;
      } catch (error) { console.error('Wallet connection error:', error); return false; }
    } else { console.error('No Ethereum wallet detected'); return false; }
  }

  async recordChoice(choiceId, choiceText) {
    if (!this.playerAddress) { console.error('Wallet not connected'); return false; }
    try {
      const contract = new web3.eth.Contract(gameABI, this.contractAddress);
      const result = await contract.methods.recordPlayerChoice(choiceId, choiceText).send({ from: this.playerAddress });
      this.significantChoices.push({ id: choiceId, text: choiceText, timestamp: Date.now() });
      return true;
    } catch (error) { console.error('Error recording choice:', error); return false; }
  }

  async loadPlayerChoices() {
    if (!this.playerAddress) return [];
    try {
      const contract = new web3.eth.Contract(gameABI, this.contractAddress);
      const choices = await contract.methods.getPlayerChoices(this.playerAddress).call();
      this.significantChoices = choices.map(choice => ({ id: choice.choiceId, text: choice.choiceText, timestamp: parseInt(choice.timestamp) * 1000 }));
      return this.significantChoices;
    } catch (error) { console.error('Error loading choices:', error); return []; }
  }

  getPlayerStoryPath() {
    const sortedChoices = [...this.significantChoices].sort((a, b) => a.timestamp - b.timestamp);
    return sortedChoices.map(choice => choice.text).join(' → ');
  }

  hasPlayerMadeChoice(choiceId) { return this.significantChoices.some(choice => choice.id === choiceId); }
}
```

Also included are patterns for minting game items, retrieving player items, and managing NFT-based inventories (see the examples for BlockchainInventory and gameItemsABI).
{% endtab %}
{% endtabs %}

***

### Idle Games

Idle (incremental) games center on automated resource generation and progression systems: generators, upgrades, offline progress, prestige, and save systems.

{% tabs %}
{% tab title="Game Loops" %}
#### Idle Game Loops and Resource Generation

Basic idle model:

```javascript
class IdleGame {
  constructor() {
    this.resources = { gold: 0, gems: 0 };
    this.generators = {
      miners: { count: 0, baseCost: 10, baseOutput: 0.1, costMultiplier: 1.15 },
      gemMiners: { count: 0, baseCost: 100, baseOutput: 0.05, costMultiplier: 1.18 }
    };
    this.lastUpdate = Date.now();
    this.offlineProgressEnabled = true;
    this.startGameLoop();
  }

  startGameLoop() { setInterval(() => this.update(), 100); } // 10x/sec

  update() {
    const now = Date.now();
    const deltaTime = (now - this.lastUpdate) / 1000; this.lastUpdate = now;
    this.generateResources(deltaTime);
    this.updateUI();
  }

  generateResources(deltaTime) {
    const goldPerSecond = this.generators.miners.count * this.generators.miners.baseOutput;
    this.resources.gold += goldPerSecond * deltaTime;
    const gemsPerSecond = this.generators.gemMiners.count * this.generators.gemMiners.baseOutput;
    this.resources.gems += gemsPerSecond * deltaTime;
  }

  buyGenerator(type, amount = 1) {
    const generator = this.generators[type]; if (!generator) return false;
    let totalCost = 0;
    for (let i = 0; i < amount; i++) totalCost += Math.floor(generator.baseCost * Math.pow(generator.costMultiplier, generator.count + i));
    if (this.resources.gold < totalCost) return false;
    this.resources.gold -= totalCost; generator.count += amount; this.updateUI(); return true;
  }

  calculateOfflineProgress() { /* uses lastPlayTime from localStorage and caps progress */ }

  saveGame() { localStorage.setItem('lastPlayTime', Date.now().toString()); localStorage.setItem('gameState', JSON.stringify({ resources: this.resources, generators: this.generators })); }

  loadGame() { /* loads and calculates offline progress */ }
}
```
{% endtab %}

{% tab title="Progress Systems" %}
#### Designing Progress Systems

Upgrades system (multipliers, prerequisites) and prestige patterns:

* UpgradeSystem example (upgrade definitions, visibility, purchase checks, applying effects).
* PrestigeSystem example (calculate prestige points, perform reset, apply permanent bonuses).

Key patterns:

* Visible vs available: show upgrades when prerequisites met; only allow purchase when cost is affordable.
* Multipliers and cost reduction stacking: multiply or add depending on intended stacking rules.
* Prestige: reset progress in exchange for permanent bonuses, unlock new features.

(See original code blocks for concrete classes and algorithms.)
{% endtab %}

{% tab title="Save Systems" %}
#### Data Persistence and Save Systems

Comprehensive save/load approach with autosave, compatibility/version checks, offline progress calculation, import/export:

* SaveSystem class: autosave interval, visibility handlers, beforeunload save, save()/load() with version checks, calculateOfflineProgress(lastTimestamp), exportSave(), importSave(), clearSave().

Important points:

* Store timestamp + version + full state.
* Cap offline progress and recalculate using saved production rates.
* Provide export/import via base64 for manual backups.
{% endtab %}

{% tab title="Blockchain Integration" %}
#### Blockchain Integration for Idle Games

Tokenizing resources, syncing off-chain progress to on-chain tokens, minting, withdrawing, and auto-sync strategies:

* Track offchainPending resources and sync to blockchain when thresholds met.
* Connect to wallet (MetaMask), use web3 to call mintGameTokens/mintGameItem/burnAndWithdraw, and keep UI status indicators.
* Use periodic autoSync and thresholds to limit gas usage.

Example class: BlockchainIdleGame (defines syncThreshold, autoSyncInterval, generateResources, syncToBlockchain, loadPlayerTokens, withdrawTokens).
{% endtab %}
{% endtabs %}

***

### Incremental Games

Incremental games emphasize active and layered progression (upgrades trees, converters, multi-resource economy). They build on idle game concepts with more depth.

{% tabs %}
{% tab title="Economy Design" %}
#### Designing Incremental Game Economies

Key components:

* Multi-resource systems (coins, crystals, energy)
* Generators with unlock conditions and cost multipliers
* Converters to transform resources
* Modifiers and multipliers applied from upgrades

Example skeleton: GameEconomy class that processes generators, converters, energy regeneration, click interactions, buy logic, and unlock checking.
{% endtab %}

{% tab title="Upgrade Systems" %}
#### Building Complex Upgrade Systems

Advanced upgrade trees include:

* Categories (production, click, economy, capacity)
* Dynamic cost functions, level-stacking, requirements (upgrades, resource thresholds)
* Availability and visibility separation
* Purchase flow applying effects and updating status

Example: UpgradeSystem class with updateUpgradeStatus(), checkRequirements(), purchaseUpgrade(), getVisibleUpgrades().
{% endtab %}

{% tab title="Balancing" %}
#### Game Balancing Techniques

Balance manager responsibilities:

* Define target progression times (timeToFirstBuilding, firstUpgrade, firstPrestige)
* Calculate building/upgrade costs relative to production rates and target times
* Track analytics (playTime, resources earned, buildings purchased) and generate suggestions for balancing
* Compute prestige rewards and provide suggestions when progression is too fast/slow

Example: GameBalancer class with params, analytics, and methods to analyze progression and suggest adjustments.
{% endtab %}

{% tab title="Blockchain Integration" %}
#### Blockchain Integration for Incremental Games

Examples and patterns:

* NFT boosters (production multipliers, auto-clickers, offline boosters) with activation slots
* Blockchain-based prestige systems (record prestige events on-chain, track total prestige points, leaderboard)
* Minting NFT boosters, activating/deactivating boosters, applying effects to game multipliers
* On-chain prestige: performPrestige(contract) with resulting permanent bonuses and recorded history

Classes in examples: NFTBoosterSystem, BlockchainPrestigeSystem.
{% endtab %}
{% endtabs %}

***

### Puzzle Games

Puzzle games rely on solid core mechanics: grid systems, match detection, solver algorithms, level generation, and optional blockchain features for sharing levels/achievements.

{% tabs %}
{% tab title="Core Mechanics" %}
#### Puzzle Game Core Mechanics

Grid-based puzzle system (match-3 style):

```javascript
class PuzzleGrid {
  constructor(width, height) {
    this.width = width; this.height = height; this.cells = []; this.initialize();
    this.moves = 0; this.score = 0; this.gameOver = false; this.onUpdate = null;
  }
  initialize() { /* fills grid */ }
  getCell(x,y) { /* returns cell or null */ }
  swapCells(x1,y1,x2,y2) { /* swaps cells and increments moves */ }
  fillRandom(valueGenerator) { /* fills with random values */ }
  checkMatches(minMatchLength = 3) { /* returns list of matches horizontal/vertical */ }
  clearMatches(matches) { /* clears and scores matches */ }
  applyGravity() { /* lets cells fall down */ }
  fillEmptySpaces(valueGenerator) { /* fills from top */ }
  serialize() { return JSON.stringify({ width:this.width, height:this.height, cells:this.cells, score:this.score, moves:this.moves, gameOver:this.gameOver }); }
  static deserialize(json) { /* returns PuzzleGrid or null */ }
}
```

Match types and special gem behavior (power gem, rainbow gem, bomb gem) are described in the examples.
{% endtab %}

{% tab title="Level Generation" %}
#### Level Generation

Patterns and approaches:

* Procedural random fill with checks to ensure solvable states
* Seeded generation to reproduce levels
* Constraints to avoid immediate matches on create (for match-3)
* Difficulty ramps via distribution, obstacles, and required match counts

(See code examples for grid initialization and refill logic.)
{% endtab %}

{% tab title="Solver Algorithms" %}
#### Solver Algorithms

Common solver approaches:

* Flood fill / BFS for reachability and area detection
* A\* for path-based puzzles and sliding blocks
* Backtracking and constraint propagation for logic puzzles (Sudoku-like)
* Heuristics to generate hints (find the best match or next move)

Implementations depend on puzzle rules; grid abstraction above supports these algorithmic layers.
{% endtab %}

{% tab title="Blockchain Integration" %}
#### Blockchain Integration for Puzzle Games

Use cases:

* Minting puzzle levels as NFTs (author-owned, tradable)
* Leaderboards and verifiable solutions recorded on-chain
* Challenge NFTs that pay out to first solver or top scorers

Patterns:

* Store minimal metadata (level seed, hash of solution) on-chain to save gas
* Use off-chain content hosting for big payloads, storing URIs in token metadata
* Verify attempts off-chain, submit proofs/score transactions on-chain for rewards
{% endtab %}
{% endtabs %}

***

Notes

* Code examples are provided verbatim (no URLs modified).
* The original page includes interactive demo canvases and UI elements; those are represented in the examples as code snippets and class patterns to reproduce in your projects.
* Blockchain examples assume you will wire them up with a suitable web3 provider (web3.js / ethers.js) and smart contract ABIs & addresses.

If you want, I can:

* Convert any specific section into a GitBook stepper (e.g., walk-through to build a simple canvas game).
* Extract only the code examples into separate pages/files (one per topic) for easier import.
* Create tabs per code language (if you have multi-language code examples) or produce a simplified quickstart (minimal runnable example) for canvas or idle games.
