<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS3 & JavaScript Magic</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Interactive Playground</h1>
    </header>

    <main>
        <!-- Theme Selector with LocalStorage -->
        <section class="theme-section">
            <h2>Theme Preferences</h2>
            <div class="theme-options">
                <button class="theme-btn light" data-theme="light">Light</button>
                <button class="theme-btn dark" data-theme="dark">Dark</button>
                <button class="theme-btn rainbow" data-theme="rainbow">Rainbow</button>
            </div>
            <p>Your preference will be remembered!</p>
        </section>

        <!-- Animated Elements -->
        <section class="animation-section">
            <h2>Animation Zone</h2>
            
            <div class="animation-box" id="hover-animation">
                <p>Hover over me!</p>
            </div>

            <button id="click-animation-btn" class="magic-btn">Click for Magic</button>
            <div class="animated-object" id="animated-object"></div>
        </section>

        <!-- Counter with Persistence -->
        <section class="counter-section">
            <h2>Persistent Counter</h2>
            <div class="counter-display" id="counter">0</div>
            <div class="counter-controls">
                <button id="increment-btn">+</button>
                <button id="decrement-btn">-</button>
                <button id="reset-btn">Reset</button>
            </div>
        </section>
    </main>

    <script src="script.js"></script>
</body>
</html>

/* Base Styles */
:root {
    --primary-color: #3498db;
    --bg-color: #f9f9f9;
    --text-color: #333;
    --transition-speed: 0.4s;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: var(--bg-color);
    color: var(--text-color);
    line-height: 1.6;
    padding: 20px;
    transition: background-color var(--transition-speed), color var(--transition-speed);
}

/* Theme Styles */
body.dark {
    --primary-color: #9b59b6;
    --bg-color: #2c3e50;
    --text-color: #ecf0f1;
}

body.rainbow {
    animation: rainbowBg 10s infinite;
}

@keyframes rainbowBg {
    0% { background-color: #ff9a9e; }
    14% { background-color: #fad0c4; }
    28% { background-color: #fbc2eb; }
    42% { background-color: #a6c1ee; }
    57% { background-color: #84fab0; }
    71% { background-color: #f6d365; }
    85% { background-color: #fda085; }
    100% { background-color: #ff9a9e; }
}

/* Theme Buttons */
.theme-options {
    display: flex;
    gap: 10px;
    margin: 20px 0;
}

.theme-btn {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: transform 0.3s, box-shadow 0.3s;
}

.theme-btn:hover {
    transform: translateY(-3px);
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.theme-btn.light {
    background-color: #f9f9f9;
    color: #333;
}

.theme-btn.dark {
    background-color: #2c3e50;
    color: white;
}

.theme-btn.rainbow {
    background: linear-gradient(90deg, 
        #ff9a9e, #fad0c4, #fbc2eb, #a6c1ee, 
        #84fab0, #f6d365, #fda085);
    color: #333;
}

/* Animation Section */
.animation-box {
    width: 200px;
    height: 200px;
    background-color: var(--primary-color);
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 20px auto;
    border-radius: 8px;
    transition: all var(--transition-speed) ease;
}

.animation-box:hover {
    transform: rotate(15deg) scale(1.1);
    background-color: #e74c3c;
}

.magic-btn {
    padding: 12px 24px;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    display: block;
    margin: 20px auto;
    transition: background-color 0.3s;
}

.magic-btn:hover {
    background-color: #2980b9;
}

.animated-object {
    width: 100px;
    height: 100px;
    background-color: #2ecc71;
    margin: 30px auto;
    border-radius: 50%;
    opacity: 0;
}

/* Counter Section */
.counter-section {
    text-align: center;
    margin-top: 40px;
}

.counter-display {
    font-size: 3rem;
    margin: 20px 0;
    color: var(--primary-color);
    transition: transform 0.2s;
}

.counter-controls {
    display: flex;
    justify-content: center;
    gap: 15px;
}

.counter-controls button {
    padding: 10px 20px;
    font-size: 1.2rem;
    background-color: var(--primary-color);
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: transform 0.2s;
}

.counter-controls button:hover {
    transform: scale(1.1);
}

/* Animation Classes */
@keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-50px); }
}

@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}

.animate-bounce {
    animation: bounce 1s ease infinite;
    opacity: 1 !important;
}

.animate-spin {
    animation: spin 2s linear infinite;
    opacity: 1 !important;
}

.animate-fade {
    animation: fadeIn 1s ease forwards;
}

@keyframes fadeIn {
    from { opacity: 0; transform: scale(0.5); }
    to { opacity: 1; transform: scale(1); }
}
// DOM Elements
const themeButtons = document.querySelectorAll('.theme-btn');
const hoverAnimationBox = document.getElementById('hover-animation');
const clickAnimationBtn = document.getElementById('click-animation-btn');
const animatedObject = document.getElementById('animated-object');
const counterDisplay = document.getElementById('counter');
const incrementBtn = document.getElementById('increment-btn');
const decrementBtn = document.getElementById('decrement-btn');
const resetBtn = document.getElementById('reset-btn');

// 1. Theme Selection with LocalStorage
function setTheme(theme) {
    document.body.className = theme;
    localStorage.setItem('preferredTheme', theme);
}

// Load saved theme
const savedTheme = localStorage.getItem('preferredTheme') || 'light';
setTheme(savedTheme);

// Theme button event listeners
themeButtons.forEach(button => {
    button.addEventListener('click', () => {
        const theme = button.dataset.theme;
        setTheme(theme);
        
        // Add visual feedback
        button.style.transform = 'scale(0.95)';
        setTimeout(() => {
            button.style.transform = '';
        }, 200);
    });
});

// 2. Interactive Animations
// Hover animation
hoverAnimationBox.addEventListener('mouseenter', () => {
    hoverAnimationBox.style.boxShadow = '0 10px 20px rgba(0,0,0,0.2)';
});

hoverAnimationBox.addEventListener('mouseleave', () => {
    hoverAnimationBox.style.boxShadow = '';
});

// Click animation
const animationTypes = ['bounce', 'spin', 'fade'];
let currentAnimation = 0;

clickAnimationBtn.addEventListener('click', () => {
    // Remove previous animation classes
    animatedObject.classList.remove('animate-bounce', 'animate-spin', 'animate-fade');
    
    // Add new animation
    const animationClass = `animate-${animationTypes[currentAnimation]}`;
    animatedObject.classList.add(animationClass);
    
    // Cycle through animations
    currentAnimation = (currentAnimation + 1) % animationTypes.length;
    
    // Button feedback
    clickAnimationBtn.textContent = `Next: ${animationTypes[currentAnimation]}`;
    clickAnimationBtn.style.backgroundColor = getRandomColor();
});

function getRandomColor() {
    const colors = ['#e74c3c', '#9b59b6', '#3498db', '#2ecc71', '#f1c40f', '#e67e22'];
    return colors[Math.floor(Math.random() * colors.length)];
}

// 3. Persistent Counter with LocalStorage
let count = parseInt(localStorage.getItem('savedCount')) || 0;
counterDisplay.textContent = count;

function updateCounter(value) {
    count = value;
    counterDisplay.textContent = count;
    localStorage.setItem('savedCount', count.toString());
    
    // Add visual feedback
    counterDisplay.style.transform = 'scale(1.2)';
    setTimeout(() => {
        counterDisplay.style.transform = 'scale(1)';
    }, 200);
}

incrementBtn.addEventListener('click', () => {
    updateCounter(count + 1);
});

decrementBtn.addEventListener('click', () => {
    updateCounter(Math.max(0, count - 1));
});

resetBtn.addEventListener('click', () => {
    updateCounter(0);
});

// Bonus: Page load animation
document.addEventListener('DOMContentLoaded', () => {
    document.body.style.opacity = '0';
    setTimeout(() => {
        document.body.style.transition = 'opacity 0.5s ease';
        document.body.style.opacity = '1';
    }, 100);
});
