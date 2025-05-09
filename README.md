<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BioEngineer: Interactive Biology Games</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/tailwindcss/2.2.19/tailwind.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        @keyframes glow {
            0% { box-shadow: 0 0 5px #4ade80; }
            50% { box-shadow: 0 0 20px #4ade80; }
            100% { box-shadow: 0 0 5px #4ade80; }
        }
        
        .bio-glow {
            animation: glow 3s infinite;
        }
        
        .gene-segment {
            height: 30px;
            transition: all 0.3s ease;
        }
        
        .gene-segment:hover {
            transform: translateY(-3px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .nucleotide {
            width: 40px;
            height: 40px;
            margin: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.2s ease;
        }
        
        .nucleotide:hover {
            transform: scale(1.1);
        }
        
        .nucleotide-A { background-color: #60a5fa; }
        .nucleotide-T { background-color: #f87171; }
        .nucleotide-G { background-color: #4ade80; }
        .nucleotide-C { background-color: #fbbf24; }
        
        .tab-button {
            @apply font-medium text-center px-4 py-2 rounded-t-lg transition duration-200;
        }
        
        .tab-button.active {
            @apply bg-gray-800 text-white;
        }
        
        .tab-button:not(.active) {
            @apply bg-gray-700 text-gray-300 hover:bg-gray-600;
        }
        
        .game-container {
            min-height: 80vh;
        }
    </style>
</head>
<body class="bg-gray-900 text-gray-100 min-h-screen">
    <!-- Header with game selection tabs -->
    <header class="bg-gray-800 border-b border-green-500 sticky top-0 z-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
            <div class="flex items-center justify-between">
                <h1 class="text-xl font-bold flex items-center">
                    <svg class="h-8 w-8 text-green-400 mr-2" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M4 19H20M4 5H20M4 12H20M16 5V19M8 5V19" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                    </svg>
                    BioEngineer Games
                </h1>
                
                <div class="flex space-x-2">
                    <button id="crispr-tab" class="tab-button active">CRISPR Lab</button>
                    <button id="ecosystem-tab" class="tab-button">Ecosystem Builder</button>
                    <button id="virus-tab" class="tab-button">Virus Outbreak</button>
                    <button id="evolution-tab" class="tab-button">Evolution Arena</button>
                </div>
            </div>
        </div>
    </header>

    <!-- Game Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <!-- CRISPR Lab Game -->
        <section id="crispr-game" class="game-container">
            <div class="bg-gray-800 rounded-lg shadow-xl overflow-hidden">
                <div class="px-6 py-8">
                    <h2 class="text-2xl font-bold text-center text-white mb-6">CRISPR Gene-Editing Lab</h2>
                    
                    <div class="flex flex-wrap">
                        <div class="w-full lg:w-1/3 pr-0 lg:pr-8">
                            <h3 class="text-xl font-bold text-white mb-4">Challenge: Fix Cystic Fibrosis Gene</h3>
                            <p class="text-gray-300 mb-6">
                                Cystic fibrosis is caused by mutations in the CFTR gene. Your task is to identify and correct the most common mutation (F508del) using CRISPR-Cas9 technology.
                            </p>
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-green-400 font-medium mb-2">Objective</h4>
                                <p class="text-gray-300 text-sm">
                                    Replace the defective gene sequence with a functional one without introducing unwanted mutations.
                                </p>
                            </div>
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-green-400 font-medium mb-2">Tools Available</h4>
                                <ul class="text-gray-300 text-sm space-y-2">
                                    <li class="flex items-center">
                                        <svg class="h-4 w-4 text-green-400 mr-2" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                            <path d="M5 13L9 17L19 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                        </svg>
                                        CRISPR-Cas9 System
                                    </li>
                                    <li class="flex items-center">
                                        <svg class="h-4 w-4 text-green-400 mr-2" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                            <path d="M5 13L9 17L19 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                        </svg>
                                        Guide RNA Designer
                                    </li>
                                    <li class="flex items-center">
                                        <svg class="h-4 w-4 text-green-400 mr-2" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                                            <path d="M5 13L9 17L19 7" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                                        </svg>
                                        DNA Sequence Analyzer
                                    </li>
                                </ul>
                            </div>
                            <button id="start-challenge" class="w-full bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                Start Challenge
                            </button>
                        </div>
                        <div class="w-full lg:w-2/3 mt-8 lg:mt-0">
                            <div class="bg-gray-700 p-6 rounded-lg h-full">
                                <div class="flex justify-between items-center mb-6">
                                    <h3 class="text-xl font-bold text-white">Gene Editor</h3>
                                    <div class="flex space-x-2">
                                        <button id="analyze-button" class="bg-blue-600 hover:bg-blue-700 text-xs text-white px-3 py-1 rounded transform transition hover:scale-105">Analyze</button>
                                        <button id="test-fix-button" class="bg-green-600 hover:bg-green-700 text-xs text-white px-3 py-1 rounded transform transition hover:scale-105">Test Fix</button>
                                    </div>
                                </div>
                                
                                <!-- DNA Visualization -->
                                <div class="flex items-center justify-center mb-6">
                                    <div class="relative w-full h-16 flex items-center">
                                        <div class="absolute inset-0">
                                            <svg class="w-full h-full" viewBox="0 0 800 60" xmlns="http://www.w3.org/2000/svg">
                                                <path d="M0,30 Q20,5 40,30 Q60,55 80,30 Q100,5 120,30 Q140,55 160,30 Q180,5 200,30 Q220,55 240,30 Q260,5 280,30 Q300,55 320,30 Q340,5 360,30 Q380,55 400,30 Q420,5 440,30 Q460,55 480,30 Q500,5 520,30 Q540,55 560,30 Q580,5 600,30 Q620,55 640,30 Q660,5 680,30 Q700,55 720,30 Q740,5 760,30 Q780,55 800,30" stroke="#4ade80" stroke-width="2" fill="none"/>
                                                <path d="M0,30 Q20,55 40,30 Q60,5 80,30 Q100,55 120,30 Q140,5 160,30 Q180,55 200,30 Q220,5 240,30 Q260,55 280,30 Q300,5 320,30 Q340,55 360,30 Q380,5 400,30 Q420,55 440,30 Q460,5 480,30 Q500,55 520,30 Q540,5 560,30 Q580,55 600,30 Q620,5 640,30 Q660,55 680,30 Q700,5 720,30 Q740,55 760,30 Q780,5 800,30" stroke="#4ade80" stroke-width="2" fill="none"/>
                                            </svg>
                                        </div>
                                        
                                        <!-- Mutation Highlight -->
                                        <div class="absolute left-1/2 transform -translate-x-1/2 -translate-y-1/2 top-1/2 w-32 h-12 border-2 border-red-500 rounded bg-red-900 bg-opacity-30 flex items-center justify-center">
                                            <span class="text-red-400 text-xs font-medium">F508del Mutation</span>
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- Gene Sequence Editor -->
                                <div class="mb-6">
                                    <label class="block text-sm font-medium text-gray-400 mb-2">Gene Sequence Editor</label>
                                    <div class="bg-gray-900 p-4 rounded border border-gray-700 overflow-x-auto">
                                        <div class="flex flex-wrap">
                                            <div class="gene-segment flex items-center mb-2 w-full">
                                                <span class="text-gray-500 mr-2 w-12 text-sm">1</span>
                                                <div class="flex-1 flex">
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-G">G</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-G">G</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                </div>
                                            </div>
                                            <div class="gene-segment flex items-center mb-2 w-full">
                                                <span class="text-gray-500 mr-2 w-12 text-sm">9</span>
                                                <div class="flex-1 flex">
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <span class="nucleotide nucleotide-G">G</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                </div>
                                            </div>
                                            <div class="gene-segment flex items-center mb-2 w-full bg-red-900 bg-opacity-30 rounded">
                                                <span class="text-gray-500 mr-2 w-12 text-sm">17</span>
                                                <div class="flex-1 flex">
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <!-- Deletion highlighted with an empty space -->
                                                    <span id="mutation-spot" class="nucleotide bg-red-500 opacity-50">—</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                </div>
                                            </div>
                                            <div class="gene-segment flex items-center mb-2 w-full">
                                                <span class="text-gray-500 mr-2 w-12 text-sm">25</span>
                                                <div class="flex-1 flex">
                                                    <span class="nucleotide nucleotide-C">C</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-G">G</span>
                                                    <span class="nucleotide nucleotide-G">G</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                    <span class="nucleotide nucleotide-T">T</span>
                                                    <span class="nucleotide nucleotide-A">A</span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- CRISPR Tools -->
                                <div>
                                    <div class="flex justify-between items-center mb-4">
                                        <label class="block text-sm font-medium text-gray-400">CRISPR Tools</label>
                                        <button id="guide-rna-button" class="text-xs bg-purple-600 hover:bg-purple-700 text-white px-3 py-1 rounded transform transition hover:scale-105">Create Guide RNA</button>
                                    </div>
                                    <div class="grid grid-cols-2 gap-4">
                                        <div class="bg-gray-900 p-3 rounded border border-gray-700">
                                            <h4 class="text-sm font-medium text-purple-400 mb-2">Cas9 Nuclease</h4>
                                            <p class="text-xs text-gray-400">Cuts DNA at a specific location guided by RNA.</p>
                                            <button id="select-cas9" class="mt-2 w-full bg-gray-700 hover:bg-gray-600 text-xs py-1 rounded transform transition hover:scale-105">Select</button>
                                        </div>
                                        <div class="bg-gray-900 p-3 rounded border border-gray-700">
                                            <h4 class="text-sm font-medium text-purple-400 mb-2">Donor Template</h4>
                                            <p class="text-xs text-gray-400">Provides correct DNA sequence for repair.</p>
                                            <button id="design-template" class="mt-2 w-full bg-gray-700 hover:bg-gray-600 text-xs py-1 rounded transform transition hover:scale-105">Design</button>
                                        </div>
                                    </div>
                                </div>

                                <!-- Results Panel (Hidden by default) -->
                                <div id="crispr-results" class="mt-6 bg-gray-900 p-4 rounded border border-gray-700 hidden">
                                    <h4 class="text-green-400 font-medium mb-2">Simulation Results</h4>
                                    <div id="crispr-result-content" class="text-gray-300"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Ecosystem Builder Game -->
        <section id="ecosystem-game" class="game-container hidden">
            <div class="bg-gray-800 rounded-lg shadow-xl overflow-hidden">
                <div class="px-6 py-8">
                    <h2 class="text-2xl font-bold text-center text-white mb-6">Ecosystem Builder</h2>
                    
                    <div class="flex flex-wrap">
                        <div class="w-full lg:w-1/3 pr-0 lg:pr-8">
                            <h3 class="text-xl font-bold text-white mb-4">Challenge: Build a Rainforest</h3>
                            <p class="text-gray-300 mb-6">
                                Create a balanced rainforest ecosystem that can sustain itself over time.
                            </p>
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-green-400 font-medium mb-2">Available Species</h4>
                                <div class="space-y-2">
                                    <div class="species-item bg-gray-600 p-2 rounded flex items-center cursor-pointer transform transition hover:scale-105" data-species="tree">
                                        <div class="w-8 h-8 bg-green-800 rounded-full flex items-center justify-center mr-2">
                                            <span class="text-green-300">🌳</span>
                                        </div>
                                        <div>
                                            <h5 class="text-white text-sm">Rainforest Tree</h5>
                                            <p class="text-xs text-gray-400">Producer</p>
                                        </div>
                                    </div>
                                    <div class="species-item bg-gray-600 p-2 rounded flex items-center cursor-pointer transform transition hover:scale-105" data-species="herbivore">
                                        <div class="w-8 h-8 bg-yellow-800 rounded-full flex items-center justify-center mr-2">
                                            <span class="text-yellow-300">🦋</span>
                                        </div>
                                        <div>
                                            <h5 class="text-white text-sm">Butterflies</h5>
                                            <p class="text-xs text-gray-400">Herbivore</p>
                                        </div>
                                    </div>
                                    <div class="species-item bg-gray-600 p-2 rounded flex items-center cursor-pointer transform transition hover:scale-105" data-species="carnivore">
                                        <div class="w-8 h-8 bg-red-800 rounded-full flex items-center justify-center mr-2">
                                            <span class="text-red-300">🦎</span>
                                        </div>
                                        <div>
                                            <h5 class="text-white text-sm">Lizard</h5>
                                            <p class="text-xs text-gray-400">Carnivore</p>
                                        </div>
                                    </div>
                                    <div class="species-item bg-gray-600 p-2 rounded flex items-center cursor-pointer transform transition hover:scale-105" data-species="apex">
                                        <div class="w-8 h-8 bg-purple-800 rounded-full flex items-center justify-center mr-2">
                                            <span class="text-purple-300">🐆</span>
                                        </div>
                                        <div>
                                            <h5 class="text-white text-sm">Jaguar</h5>
                                            <p class="text-xs text-gray-400">Apex Predator</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="flex space-x-2">
                                <button id="run-ecosystem" class="flex-1 bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                    Run Simulation
                                </button>
                                <button id="reset-ecosystem" class="bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                    Reset
                                </button>
                            </div>
                            <button id="balance-ecosystem" class="w-full mt-2 bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                Auto-Balance
                            </button>
                        </div>
                        <div class="w-full lg:w-2/3 mt-8 lg:mt-0">
                            <div class="bg-gray-700 p-6 rounded-lg h-full">
                                <!-- Ecosystem Canvas -->
                                <div class="mb-6 relative">
                                    <div id="ecosystem-canvas" class="w-full h-64 bg-green-900 bg-opacity-30 rounded border border-green-800 flex flex-wrap p-4">
                                        <div class="absolute inset-0 flex items-center justify-center text-gray-400 ecosystem-placeholder">
                                            Drag species here to populate your ecosystem
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- Population Graph -->
                                <div class="mb-6">
                                    <h4 class="text-sm font-medium text-gray-400 mb-2">Population Trends</h4>
                                    <div id="population-graph" class="w-full h-48 bg-gray-900 rounded border border-gray-700 p-2">
                                        <canvas id="ecosystem-chart" class="w-full h-full"></canvas>
                                    </div>
                                </div>
                                
                                <div id="ecosystem-status" class="mt-4 p-3 rounded bg-gray-900 text-gray-300 text-sm">
                                    Ecosystem status: Ready to simulate
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Virus Outbreak Game -->
        <section id="virus-game" class="game-container hidden">
            <div class="bg-gray-800 rounded-lg shadow-xl overflow-hidden">
                <div class="px-6 py-8">
                    <h2 class="text-2xl font-bold text-center text-white mb-6">Virus Outbreak Simulator</h2>
                    
                    <div class="flex flex-wrap">
                        <div class="w-full lg:w-1/3 pr-0 lg:pr-8">
                            <h3 class="text-xl font-bold text-white mb-4">Virus Control Panel</h3>
                            
                            <!-- Virus Parameters -->
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-red-400 font-medium mb-2">Virus Parameters</h4>
                                <div class="space-y-4">
                                    <div>
                                        <label class="block text-sm text-gray-400 mb-1">Transmission Rate</label>
                                        <input type="range" id="transmission-rate" min="1" max="10" value="5" class="w-full">
                                        <div class="flex justify-between text-xs text-gray-500">
                                            <span>Low</span>
                                            <span>High</span>
                                        </div>
                                    </div>
                                    <div>
                                        <label class="block text-sm text-gray-400 mb-1">Mutation Rate</label>
                                        <input type="range" id="mutation-rate" min="1" max="10" value="3" class="w-full">
                                        <div class="flex justify-between text-xs text-gray-500">
                                            <span>Stable</span>
                                            <span>Rapid</span>
                                        </div>
                                    </div>
                                    <div>
                                        <label class="block text-sm text-gray-400 mb-1">Severity</label>
                                        <input type="range" id="severity" min="1" max="10" value="4" class="w-full">
                                        <div class="flex justify-between text-xs text-gray-500">
                                            <span>Mild</span>
                                            <span>Severe</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Response Tools -->
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-blue-400 font-medium mb-2">Response Tools</h4>
                                <div class="space-y-2">
                                    <button id="social-distancing" class="w-full bg-blue-900 hover:bg-blue-800 text-blue-200 text-sm font-medium py-2 px-4 rounded-md mb-2 transform transition hover:scale-105">
                                        Implement Social Distancing
                                    </button>
                                    <button id="travel-restrictions" class="w-full bg-blue-900 hover:bg-blue-800 text-blue-200 text-sm font-medium py-2 px-4 rounded-md mb-2 transform transition hover:scale-105">
                                        Impose Travel Restrictions
                                    </button>
                                    <button id="develop-vaccine" class="w-full bg-blue-900 hover:bg-blue-800 text-blue-200 text-sm font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                        Develop Vaccine (20 days)
                                    </button>
                                </div>
                            </div>
                            
                            <button id="start-outbreak" class="w-full bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                Start Outbreak
                            </button>
                        </div>
                        <div class="w-full lg:w-2/3 mt-8 lg:mt-0">
                            <div class="bg-gray-700 p-6 rounded-lg h-full">
                                <div class="flex justify-between items-center mb-6">
                                    <h3 class="text-xl font-bold text-white">Global Spread Map</h3>
                                    <div>
                                        <span id="day-counter" class="text-xs bg-gray-800 text-white px-3 py-1 rounded">Day: 0</span>
                                    </div>
                                </div>
                                
                                <!-- World Map Visualization -->
                                <div class="mb-6">
                                    <div id="virus-map" class="w-full h-72 bg-gray-900 rounded border border-gray-700 relative overflow-hidden">
                                        <!-- Simplified World Map -->
                                        <svg viewBox="0 0 1000 500" class="w-full h-full">
                                            <!-- Continents - simplified shapes -->
                                            <path d="M200,150 Q250,100 300,150 Q350,200 400,150 Q450,100 500,150 L500,300 Q450,350 400,300 Q350,250 300,300 Q250,350 200,300 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="north-america" />
                                            <path d="M550,350 Q600,300 650,350 Q700,400 750,350 L750,450 Q700,500 650,450 Q600,400 550,450 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="south-america" />
                                            <path d="M500,150 Q550,100 600,150 Q650,200 700,150 L700,250 Q650,300 600,250 Q550,200 500,250 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="europe" />
                                            <path d="M700,150 Q750,100 800,150 Q850,200 900,150 L900,300 Q850,350 800,300 Q750,250 700,300 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="asia" />
                                            <path d="M650,300 Q700,250 750,300 Q800,350 850,300 L850,400 Q800,450 750,400 Q700,350 650,400 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="africa" />
                                            <path d="M850,400 Q900,350 950,400 L950,450 Q900,500 850,450 Z" fill="#374151" stroke="#4B5563" class="continent" data-region="australia" />
                                            
                                            <!-- Initial outbreak point -->
                                            <circle id="outbreak-start" cx="800" cy="200" r="8" fill="#DC2626" class="animate-pulse" />
                                        </svg>
                                    </div>
                                </div>
                                
                                <!-- Statistics -->
                                <div class="grid grid-cols-3 gap-4 mb-6">
                                    <div class="bg-gray-900 p-3 rounded border border-gray-700">
                                        <h4 class="text-xs text-gray-400 mb-1">Infections</h4>
                                        <p id="infection-count" class="text-lg text-red-400 font-bold">0</p>
                                    </div>
                                    <div class="bg-gray-900 p-3 rounded border border-gray-700">
                                        <h4 class="text-xs text-gray-400 mb-1">Recovered</h4>
                                        <p id="recovery-count" class="text-lg text-green-400 font-bold">0</p>
                                    </div>
                                    <div class="bg-gray-900 p-3 rounded border border-gray-700">
                                        <h4 class="text-xs text-gray-400 mb-1">R₀ Value</h4>
                                        <p id="r-value" class="text-lg text-yellow-400 font-bold">2.5</p>
                                    </div>
                                </div>
                                
                                <!-- Status Updates -->
                                <div>
                                    <h4 class="text-sm font-medium text-gray-400 mb-2">Status Updates</h4>
                                    <div id="virus-status-log" class="bg-gray-900 p-3 rounded border border-gray-700 h-24 overflow-y-auto text-xs text-gray-300">
                                        <p class="mb-1">System ready. Configure virus parameters and press Start Outbreak to begin.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Evolution Arena Game -->
        <section id="evolution-game" class="game-container hidden">
            <div class="bg-gray-800 rounded-lg shadow-xl overflow-hidden">
                <div class="px-6 py-8">
                    <h2 class="text-2xl font-bold text-center text-white mb-6">Evolution Arena</h2>
                    
                    <div class="flex flex-wrap">
                        <div class="w-full lg:w-1/3 pr-0 lg:pr-8">
                            <h3 class="text-xl font-bold text-white mb-4">Trait Selection</h3>
                            
                            <!-- Environment Selection -->
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-blue-400 font-medium mb-2">Select Environment</h4>
                                <select id="environment-select" class="w-full bg-gray-900 text-white border border-gray-600 rounded p-2">
                                    <option value="desert">Desert (High Heat, Low Water)</option>
                                    <option value="arctic">Arctic (Extreme Cold)</option>
                                    <option value="ocean">Deep Ocean (High Pressure, Low Light)</option>
                                    <option value="volcanic">Volcanic (High Acidity, Heat)</option>
                                </select>
                            </div>
                            
                            <!-- Trait Points -->
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <div class="flex justify-between items-center">
                                    <h4 class="text-blue-400 font-medium">Available Trait Points</h4>
                                    <span id="trait-points" class="text-white font-bold">10</span>
                                </div>
                            </div>
                            
                            <!-- Traits -->
                            <div class="bg-gray-700 p-4 rounded-lg mb-6">
                                <h4 class="text-blue-400 font-medium mb-2">Assign Traits</h4>
                                <div class="space-y-4">
                                    <div>
                                        <div class="flex justify-between items-center mb-1">
                                            <label class="text-sm text-gray-400">Heat Resistance</label>
                                            <div class="flex items-center">
                                                <button data-trait="heat" data-action="decrease" class="trait-btn px-2 bg-gray-900 rounded-l text-white transform transition hover:scale-110">-</button>
                                                <span id="heat-value" class="trait-value px-3 bg-gray-800 text-white">0</span>
                                                <button data-trait="heat" data-action="increase" class="trait-btn px-2 bg-gray-900 rounded-r text-white transform transition hover:scale-110">+</button>
                                            </div>
                                        </div>
                                    </div>
                                    <div>
                                        <div class="flex justify-between items-center mb-1">
                                            <label class="text-sm text-gray-400">Cold Resistance</label>
                                            <div class="flex items-center">
                                                <button data-trait="cold" data-action="decrease" class="trait-btn px-2 bg-gray-900 rounded-l text-white transform transition hover:scale-110">-</button>
                                                <span id="cold-value" class="trait-value px-3 bg-gray-800 text-white">0</span>
                                                <button data-trait="cold" data-action="increase" class="trait-btn px-2 bg-gray-900 rounded-r text-white transform transition hover:scale-110">+</button>
                                            </div>
                                        </div>
                                    </div>
                                    <div>
                                        <div class="flex justify-between items-center mb-1">
                                            <label class="text-sm text-gray-400">Water Conservation</label>
                                            <div class="flex items-center">
                                                <button data-trait="water" data-action="decrease" class="trait-btn px-2 bg-gray-900 rounded-l text-white transform transition hover:scale-110">-</button>
                                                <span id="water-value" class="trait-value px-3 bg-gray-800 text-white">0</span>
                                                <button data-trait="water" data-action="increase" class="trait-btn px-2 bg-gray-900 rounded-r text-white transform transition hover:scale-110">+</button>
                                            </div>
                                        </div>
                                    </div>
                                    <div>
                                        <div class="flex justify-between items-center mb-1">
                                            <label class="text-sm text-gray-400">Pressure Tolerance</label>
                                            <div class="flex items-center">
                                                <button data-trait="pressure" data-action="decrease" class="trait-btn px-2 bg-gray-900 rounded-l text-white transform transition hover:scale-110">-</button>
                                                <span id="pressure-value" class="trait-value px-3 bg-gray-800 text-white">0</span>
                                                <button data-trait="pressure" data-action="increase" class="trait-btn px-2 bg-gray-900 rounded-r text-white transform transition hover:scale-110">+</button>
                                            </div>
                                        </div>
                                    </div>
                                    <div>
                                        <div class="flex justify-between items-center mb-1">
                                            <label class="text-sm text-gray-400">Acid Resistance</label>
                                            <div class="flex items-center">
                                                <button data-trait="acid" data-action="decrease" class="trait-btn px-2 bg-gray-900 rounded-l text-white transform transition hover:scale-110">-</button>
                                                <span id="acid-value" class="trait-value px-3 bg-gray-800 text-white">0</span>
                                                <button data-trait="acid" data-action="increase" class="trait-btn px-2 bg-gray-900 rounded-r text-white transform transition hover:scale-110">+</button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="flex space-x-2">
                                <button id="run-evolution" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                    Run Evolution
                                </button>
                                <button id="reset-evolution" class="bg-red-600 hover:bg-red-700 text-white font-medium py-2 px-4 rounded-md transform transition hover:scale-105">
                                    Reset
                                </button>
                            </div>
                        </div>
                        <div class="w-full lg:w-2/3 mt-8 lg:mt-0">
                            <div class="bg-gray-700 p-6 rounded-lg h-full">
                                <div class="flex justify-between items-center mb-6">
                                    <h3 class="text-xl font-bold text-white">Evolution Simulator</h3>
                                    <div>
                                        <span id="generation-counter" class="text-xs bg-gray-800 text-white px-3 py-1 rounded">Generation: 0</span>
                                    </div>
                                </div>
                                
                                <!-- Organism Visualization -->
                                <div class="mb-6">
                                    <div id="organism-canvas" class="w-full h-64 bg-gray-900 rounded border border-gray-700 relative overflow-hidden">
                                        <div id="organism" class="absolute left-1/2 top-1/2 transform -translate-x-1/2 -translate-y-1/2 w-32 h-32">
                                            <svg viewBox="0 0 100 100" class="w-full h-full">
                                                <circle cx="50" cy="50" r="40" fill="#1F2937" stroke="#60A5FA" stroke-width="2" />
                                                <circle cx="35" cy="40" r="5" fill="#60A5FA" class="organism-feature" />
                                                <circle cx="65" cy="40" r="5" fill="#60A5FA" class="organism-feature" />
                                                <path d="M40,65 Q50,75 60,65" stroke="#60A5FA" stroke-width="2" fill="none" class="organism-feature" />
                                                
                                                <!-- These features will be shown/hidden based on traits -->
                                                <path id="heat-feature" class="hidden" d="M50,10 L55,20 L45,20 Z" fill="#F87171" />
                                                <path id="cold-feature" class="hidden" d="M50,90 L55,80 L45,80 Z" fill="#60A5FA" />
                                                <path id="water-feature" class="hidden" d="M10,50 L20,55 L20,45 Z" fill="#34D399" />
                                                <path id="pressure-feature" class="hidden" d="M90,50 L80,55 L80,45 Z" fill="#8B5CF6" />
                                                <path id="acid-feature" class="hidden" d="M30,20 L35,30 L25,30 Z" fill="#FBBF24" />
                                            </svg>
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- Survival Status -->
                                <div class="mb-6">
                                    <h4 class="text-sm font-medium text-gray-400 mb-2">Survival Status</h4>
                                    <div id="survival-meter" class="w-full bg-gray-800 rounded-full h-4">
                                        <div id="survival-progress" class="bg-green-600 h-4 rounded-full" style="width: 0%"></div>
                                    </div>
                                    <div class="flex justify-between text-xs text-gray-500 mt-1">
                                        <span>0%</span>
                                        <span>Survival Chance</span>
                                        <span>100%</span>
                                    </div>
                                </div>
                                
                                <!-- Evolution Log -->
                                <div>
                                    <h4 class="text-sm font-medium text-gray-400 mb-2">Evolution Log</h4>
                                    <div id="evolution-log" class="bg-gray-900 p-3 rounded border border-gray-700 h-28 overflow-y-auto text-xs text-gray-300">
                                        <p class="mb-1">Welcome to Evolution Arena. Select an environment and assign traits to begin.</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <script>
        // Tab Switching
        document.addEventListener('DOMContentLoaded', function() {
            const tabs = {
                'crispr-tab': 'crispr-game',
                'ecosystem-tab': 'ecosystem-game',
                'virus-tab': 'virus-game',
                'evolution-tab': 'evolution-game'
            };
            
            // Tab click handlers
            Object.keys(tabs).forEach(tabId => {
                document.getElementById(tabId).addEventListener('click', function() {
                    // Update tab styles
                    document.querySelectorAll('.tab-button').forEach(tab => {
                        tab.classList.remove('active');
                    });
                    this.classList.add('active');
                    
                    // Show selected game, hide others
                    Object.values(tabs).forEach(gameId => {
                        document.getElementById(gameId).classList.add('hidden');
                    });
                    document.getElementById(tabs[tabId]).classList.remove('hidden');
                });
            });
        });

        //--------------------------------------------
        // CRISPR Lab Game Functionality
        //--------------------------------------------
        let crisprGameState = {
            gameStarted: false,
            guideRNADesigned: false,
            cas9Selected: false,
            donorTemplateDesigned: false,
            mutationFixed: false,
            score: 0
        };
        
        if (document.getElementById('start-challenge')) {
            document.getElementById('start-challenge').addEventListener('click', function() {
                if (crisprGameState.gameStarted) {
                    alert('Challenge is already in progress!');
                    return;
                }
                
                crisprGameState.gameStarted = true;
                
                // Initialize the sequence editor
                const sequenceEditor = document.querySelector('.gene-segment.bg-red-900.bg-opacity-30');
                if (sequenceEditor) {
                    sequenceEditor.classList.add('animate-pulse');
                    setTimeout(() => {
                        sequenceEditor.classList.remove('animate-pulse');
                    }, 2000);
                }
                
                // Show a tutorial message
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                if (resultsPanel && resultsContent) {
                    resultsPanel.classList.remove('hidden');
                    resultsContent.innerHTML = `
                        <div class="text-blue-400 font-bold mb-2">Challenge Started!</div>
                        <p>Your goal is to correct the F508del mutation in the CFTR gene that causes cystic fibrosis.</p>
                        <ol class="list-decimal list-inside space-y-1 mt-2 text-sm">
                            <li>First, analyze the gene to identify the mutation</li>
                            <li>Design a guide RNA to target the mutation site</li>
                            <li>Select the Cas9 nuclease to cut the DNA</li>
                            <li>Create a donor template with the correct sequence</li>
                            <li>Test your fix to see if it works</li>
                        </ol>
                    `;
                }
                
                // Make nucleotides interactive
                document.querySelectorAll('.nucleotide').forEach(nucleotide => {
                    nucleotide.classList.add('cursor-pointer', 'transition-transform', 'hover:scale-110');
                    
                    nucleotide.addEventListener('click', function() {
                        // Toggle selected state
                        this.classList.toggle('ring-2');
                        this.classList.toggle('ring-white');
                        
                        // If we're clicking on the mutation spot
                        if (this.id === 'mutation-spot' && !crisprGameState.mutationFixed) {
                            // Show a context menu for editing
                            const contextMenu = document.createElement('div');
                            contextMenu.className = 'absolute z-10 bg-gray-800 shadow-lg rounded p-2 mt-2';
                            contextMenu.style.top = (this.offsetTop + this.offsetHeight) + 'px';
                            contextMenu.style.left = this.offsetLeft + 'px';
                            
                            // Only allow editing if we've gone through the proper steps
                            if (crisprGameState.guideRNADesigned && crisprGameState.cas9Selected && crisprGameState.donorTemplateDesigned) {
                                contextMenu.innerHTML = `
                                    <div class="text-xs text-white mb-1">Select nucleotide:</div>
                                    <div class="flex space-x-1">
                                        <button class="nucleotide-btn bg-blue-600 text-white w-6 h-6 rounded-full">A</button>
                                        <button class="nucleotide-btn bg-red-600 text-white w-6 h-6 rounded-full">T</button>
                                        <button class="nucleotide-btn bg-green-600 text-white w-6 h-6 rounded-full">G</button>
                                        <button class="nucleotide-btn bg-yellow-600 text-white w-6 h-6 rounded-full">C</button>
                                    </div>
                                `;
                                
                                // Add event listeners for nucleotide buttons
                                this.parentNode.appendChild(contextMenu);
                                
                                document.querySelectorAll('.nucleotide-btn').forEach(btn => {
                                    btn.addEventListener('click', function() {
                                        const nucleotide = this.textContent;
                                        const mutationSpot = document.getElementById('mutation-spot');
                                        
                                        // Update the mutation spot with the selected nucleotide
                                        mutationSpot.textContent = nucleotide;
                                        mutationSpot.classList.remove('bg-red-500', 'opacity-50');
                                        
                                        // Add appropriate class based on nucleotide
                                        switch(nucleotide) {
                                            case 'A':
                                                mutationSpot.classList.add('nucleotide-A');
                                                break;
                                            case 'T':
                                                mutationSpot.classList.add('nucleotide-T');
                                                break;
                                            case 'G':
                                                mutationSpot.classList.add('nucleotide-G');
                                                break;
                                            case 'C':
                                                mutationSpot.classList.add('nucleotide-C');
                                                break;
                                        }
                                        
                                        // Update game state
                                        crisprGameState.mutationFixed = (nucleotide === 'T'); // T is the correct nucleotide for this mutation
                                        
                                        // Remove context menu
                                        contextMenu.remove();
                                    });
                                });
                                
                                // Close context menu when clicking elsewhere
                                document.addEventListener('click', function closeMenu(e) {
                                    if (!contextMenu.contains(e.target) && e.target !== document.getElementById('mutation-spot')) {
                                        contextMenu.remove();
                                        document.removeEventListener('click', closeMenu);
                                    }
                                });
                            } else {
                                // Show message about required steps
                                contextMenu.innerHTML = `
                                    <div class="text-xs text-yellow-400 mb-1">Complete these steps first:</div>
                                    <ul class="text-xs text-gray-300 list-disc list-inside">
                                        ${!crisprGameState.guideRNADesigned ? '<li>Design guide RNA</li>' : ''}
                                        ${!crisprGameState.cas9Selected ? '<li>Select Cas9 nuclease</li>' : ''}
                                        ${!crisprGameState.donorTemplateDesigned ? '<li>Design donor template</li>' : ''}
                                    </ul>
                                `;
                                
                                this.parentNode.appendChild(contextMenu);
                                
                                // Close context menu when clicking elsewhere
                                document.addEventListener('click', function closeMenu(e) {
                                    if (!contextMenu.contains(e.target) && e.target !== document.getElementById('mutation-spot')) {
                                        contextMenu.remove();
                                        document.removeEventListener('click', closeMenu);
                                    }
                                });
                            }
                        }
                    });
                });
            });
        }
        
        if (document.getElementById('analyze-button')) {
            document.getElementById('analyze-button').addEventListener('click', function() {
                if (!crisprGameState.gameStarted) {
                    alert('Start the challenge first!');
                    return;
                }
                
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                resultsPanel.classList.remove('hidden');
                resultsContent.innerHTML = `
                    <div class="text-green-400 font-bold mb-2">Analysis Complete!</div>
                    <p>The CFTR gene contains a deletion of three nucleotides (CTT) at position 508, resulting in the loss of a phenylalanine (F) amino acid. This is known as the F508del mutation.</p>
                    <p class="mt-2">This mutation causes the CFTR protein to misfold and degrade prematurely, leading to cystic fibrosis symptoms.</p>
                    <div class="mt-3 p-2 bg-blue-900 bg-opacity-20 border border-blue-800 rounded text-sm">
                        <p class="font-medium text-blue-300">Next Step:</p>
                        <p>Design a guide RNA to target the mutation site for CRISPR-Cas9 editing.</p>
                    </div>
                `;
                
                // Highlight the mutation area
                const mutationArea = document.querySelector('.gene-segment.bg-red-900.bg-opacity-30');
                if (mutationArea) {
                    mutationArea.classList.add('animate-pulse');
                    setTimeout(() => {
                        mutationArea.classList.remove('animate-pulse');
                    }, 2000);
                }
                
                // Update score
                crisprGameState.score += 20;
                
                // Advance game state
                this.classList.add('bg-green-600');
                this.textContent = 'Analyzed ✓';
            });
        }
        
        if (document.getElementById('guide-rna-button')) {
            document.getElementById('guide-rna-button').addEventListener('click', function() {
                if (!crisprGameState.gameStarted) {
                    alert('Start the challenge first!');
                    return;
                }
                
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                resultsPanel.classList.remove('hidden');
                resultsContent.innerHTML = `
                    <div class="text-green-400 font-bold mb-2">Guide RNA Designed!</div>
                    <p>Guide RNA sequence: 5'-GTCTTACACCGTGCATCTA-3'</p>
                    <p class="mt-2">This guide RNA will direct Cas9 to cut near the F508del mutation site.</p>
                    <div class="mt-3 p-2 bg-blue-900 bg-opacity-20 border border-blue-800 rounded text-sm">
                        <p class="font-medium text-blue-300">Next Step:</p>
                        <p>Select the Cas9 nuclease to create a double-strand break at the target site.</p>
                    </div>
                `;
                
                // Update game state
                crisprGameState.guideRNADesigned = true;
                crisprGameState.score += 20;
                
                // Advance game state
                this.classList.add('bg-green-600');
                this.textContent = 'Guide RNA Created ✓';
            });
        }
        
        if (document.getElementById('select-cas9')) {
            document.getElementById('select-cas9').addEventListener('click', function() {
                if (!crisprGameState.gameStarted) {
                    alert('Start the challenge first!');
                    return;
                }
                
                if (!crisprGameState.guideRNADesigned) {
                    alert('Design a guide RNA first!');
                    return;
                }
                
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                resultsPanel.classList.remove('hidden');
                resultsContent.innerHTML = `
                    <div class="text-green-400 font-bold mb-2">Cas9 Nuclease Selected!</div>
                    <p>The Cas9 nuclease will create a double-strand break at the site targeted by your guide RNA.</p>
                    <div class="mt-3 p-2 bg-blue-900 bg-opacity-20 border border-blue-800 rounded text-sm">
                        <p class="font-medium text-blue-300">Next Step:</p>
                        <p>Design a donor template containing the correct DNA sequence to repair the mutation.</p>
                    </div>
                `;
                
                // Show cutting animation
                const mutationArea = document.querySelector('.gene-segment.bg-red-900.bg-opacity-30');
                if (mutationArea) {
                    mutationArea.classList.add('border-dashed', 'border-2', 'border-yellow-500');
                    setTimeout(() => {
                        mutationArea.classList.remove('border-dashed', 'border-2', 'border-yellow-500');
                        
                        // Flash the mutation spot
                        const mutationSpot = document.getElementById('mutation-spot');
                        if (mutationSpot) {
                            mutationSpot.classList.add('animate-pulse');
                            setTimeout(() => {
                                mutationSpot.classList.remove('animate-pulse');
                            }, 2000);
                        }
                    }, 2000);
                }
                
                // Update game state
                crisprGameState.cas9Selected = true;
                crisprGameState.score += 20;
                
                // Update button
                this.textContent = 'Selected ✓';
                this.classList.add('bg-green-700');
            });
        }
        
        if (document.getElementById('design-template')) {
            document.getElementById('design-template').addEventListener('click', function() {
                if (!crisprGameState.gameStarted) {
                    alert('Start the challenge first!');
                    return;
                }
                
                if (!crisprGameState.cas9Selected) {
                    alert('Select Cas9 nuclease first!');
                    return;
                }
                
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                resultsPanel.classList.remove('hidden');
                resultsContent.innerHTML = `
                    <div class="text-green-400 font-bold mb-2">Donor Template Designed!</div>
                    <p>The donor template contains the correct DNA sequence with the CTT codon restored at position 508.</p>
                    <div class="mt-3 p-2 bg-blue-900 bg-opacity-20 border border-blue-800 rounded text-sm">
                        <p class="font-medium text-blue-300">Next Step:</p>
                        <p>Click on the mutation site (dash symbol) and select 'T' to replace the missing nucleotide. Then test your fix.</p>
                    </div>
                `;
                
                // Update game state
                crisprGameState.donorTemplateDesigned = true;
                crisprGameState.score += 20;
                
                // Flash the mutation spot to indicate it's ready for editing
                const mutationSpot = document.getElementById('mutation-spot');
                if (mutationSpot) {
                    mutationSpot.classList.add('animate-pulse', 'cursor-pointer');
                    mutationSpot.title = "Click to edit this nucleotide";
                    setTimeout(() => {
                        mutationSpot.classList.remove('animate-pulse');
                    }, 2000);
                }
                
                // Update button
                this.textContent = 'Designed ✓';
                this.classList.add('bg-green-700');
            });
        }
        
        if (document.getElementById('test-fix-button')) {
            document.getElementById('test-fix-button').addEventListener('click', function() {
                if (!crisprGameState.gameStarted) {
                    alert('Start the challenge first!');
                    return;
                }
                
                const resultsPanel = document.getElementById('crispr-results');
                const resultsContent = document.getElementById('crispr-result-content');
                
                const mutationSpot = document.getElementById('mutation-spot');
                const isFixed = mutationSpot && mutationSpot.textContent === 'T' && mutationSpot.classList.contains('nucleotide-T');
                
                if (isFixed) {
                    resultsPanel.classList.remove('hidden');
                    resultsContent.innerHTML = `
                        <div class="text-green-400 font-bold mb-2">Success! Mutation Corrected!</div>
                        <p>The F508del mutation has been successfully corrected. The CFTR protein can now fold properly and function normally.</p>
                        <div class="mt-4 p-3 bg-green-900 bg-opacity-20 border border-green-800 rounded">
                            <div class="flex justify-between items-center">
                                <div>
                                    <p class="font-medium text-green-300">Challenge Complete!</p>
                                    <p class="text-sm text-green-200">Score: ${crisprGameState.score + 20}/100</p>
                                </div>
                                <div class="text-green-300 text-3xl font-bold">
                                    ${crisprGameState.score + 20}%
                                </div>
                            </div>
                        </div>
                        <button id="crispr-next-challenge" class="mt-4 w-full bg-purple-700 hover:bg-purple-600 text-white py-2 rounded transform transition hover:scale-105">
                            Next Challenge
                        </button>
                    `;
                    
                    document.getElementById('crispr-next-challenge').addEventListener('click', function() {
                        alert('More challenges will be available in the full game!');
                    });
                    
                    // Update game state
                    crisprGameState.mutationFixed = true;
                    crisprGameState.score += 20;
                    
                    // Complete challenge animation
                    const geneEditor = document.querySelector('.bg-gray-700.p-6.rounded-lg.h-full');
                    if (geneEditor) {
                        geneEditor.classList.add('border-2', 'border-green-500');
                        setTimeout(() => {
                            geneEditor.classList.remove('border-2', 'border-green-500');
                        }, 3000);
                    }
                } else {
                    resultsPanel.classList.remove('hidden');
                    resultsContent.innerHTML = `
                        <div class="text-red-400 font-bold mb-2">Fix Incomplete</div>
                        <p>The mutation has not been fully corrected.</p>
                        <p class="mt-2">Follow all steps to repair the gene:</p>
                        <ol class="list-decimal list-inside space-y-1 mt-2 text-sm">
                            ${!crisprGameState.guideRNADesigned ? '<li class="text-red-300">Design guide RNA</li>' : '<li class="text-green-300">Guide RNA designed ✓</li>'}
                            ${!crisprGameState.cas9Selected ? '<li class="text-red-300">Select Cas9 nuclease</li>' : '<li class="text-green-300">Cas9 selected ✓</li>'}
                            ${!crisprGameState.donorTemplateDesigned ? '<li class="text-red-300">Design donor template</li>' : '<li class="text-green-300">Donor template designed ✓</li>'}
                            <li class="text-red-300">Click on the mutation site (dash symbol) and replace it with the missing 'T' nucleotide</li>
                        </ol>
                    `;
                }
            });
        }
        
        //--------------------------------------------
        // Ecosystem Builder Game Functionality
        //--------------------------------------------
        let ecosystemGameActive = false;
        let ecosystemGameTimerId = null;
        let ecosystemDays = 0;
        let ecosystemSpecies = {'tree': 0, 'herbivore': 0, 'carnivore': 0, 'apex': 0};
        let ecosystemPopulations = {
            'tree': [0],
            'herbivore': [0],
            'carnivore': [0],
            'apex': [0]
        };
        
        // Function to update ecosystem simulation
        function updateEcosystemSimulation() {
            ecosystemDays++;
            
            // Population dynamics based on predator-prey relationships
            let newPopulations = {
                'tree': Math.max(0, ecosystemPopulations.tree[ecosystemPopulations.tree.length - 1] + 
                                (5 - ecosystemPopulations.herbivore[ecosystemPopulations.herbivore.length - 1] * 0.5)),
                'herbivore': Math.max(0, ecosystemPopulations.herbivore[ecosystemPopulations.herbivore.length - 1] + 
                                (ecosystemPopulations.tree[ecosystemPopulations.tree.length - 1] * 0.2 - 
                                 ecosystemPopulations.carnivore[ecosystemPopulations.carnivore.length - 1] * 0.5)),
                'carnivore': Math.max(0, ecosystemPopulations.carnivore[ecosystemPopulations.carnivore.length - 1] + 
                                 (ecosystemPopulations.herbivore[ecosystemPopulations.herbivore.length - 1] * 0.1 - 
                                  ecosystemPopulations.apex[ecosystemPopulations.apex.length - 1] * 0.5)),
                'apex': Math.max(0, ecosystemPopulations.apex[ecosystemPopulations.apex.length - 1] + 
                            (ecosystemPopulations.carnivore[ecosystemPopulations.carnivore.length - 1] * 0.05 - 0.2))
            };
            
            // Update populations
            for (let species in newPopulations) {
                ecosystemPopulations[species].push(Math.round(newPopulations[species]));
                // Keep only the last 30 days for the chart
                if (ecosystemPopulations[species].length > 30) {
                    ecosystemPopulations[species].shift();
                }
            }
            
            // Update the ecosystem status
            const ecosystemStatus = document.getElementById('ecosystem-status');
            if (ecosystemStatus) {
                let statusMessage = `Day ${ecosystemDays}: `;
                let balanced = true;
                
                // Check if ecosystem is balanced
                if (newPopulations.tree < 3) {
                    statusMessage += 'Trees are being depleted! ';
                    balanced = false;
                }
                
                if (newPopulations.herbivore > newPopulations.tree * 0.5) {
                    statusMessage += 'Too many herbivores for available plants. ';
                    balanced = false;
                }
                
                if (newPopulations.carnivore > newPopulations.herbivore * 0.5) {
                    statusMessage += 'Too many carnivores for available prey. ';
                    balanced = false;
                }
                
                if (newPopulations.apex > newPopulations.carnivore * 0.3) {
                    statusMessage += 'Too many apex predators for available carnivores. ';
                    balanced = false;
                }
                
                if (balanced) {
                    statusMessage += 'Ecosystem is stable.';
                    ecosystemStatus.innerHTML = `
                        <div class="text-green-400 font-bold mb-2">Stable Ecosystem!</div>
                        <p>${statusMessage}</p>
                    `;
                    ecosystemStatus.classList.add('bg-green-900', 'bg-opacity-20', 'border-green-800');
                    ecosystemStatus.classList.remove('bg-yellow-900', 'bg-opacity-20', 'border-yellow-800', 'bg-red-900', 'bg-opacity-20', 'border-red-800');
                } else {
                    // Check if any population has crashed to zero
                    let extinction = false;
                    for (let species in newPopulations) {
                        if (newPopulations[species] === 0) {
                            statusMessage = `Day ${ecosystemDays}: ${species.charAt(0).toUpperCase() + species.slice(1)}s have gone extinct! Ecosystem has collapsed.`;
                            extinction = true;
                            break;
                        }
                    }
                    
                    if (extinction) {
                        ecosystemStatus.innerHTML = `
                            <div class="text-red-400 font-bold mb-2">Ecosystem Collapse!</div>
                            <p>${statusMessage}</p>
                            <button id="restart-ecosystem" class="mt-4 bg-blue-600 hover:bg-blue-700 text-white px-3 py-1 rounded transform transition hover:scale-105">Start Over</button>
                        `;
                        ecosystemStatus.classList.add('bg-red-900', 'bg-opacity-20', 'border-red-800');
                        ecosystemStatus.classList.remove('bg-green-900', 'bg-opacity-20', 'border-green-800', 'bg-yellow-900', 'bg-opacity-20', 'border-yellow-800');
                        
                        // Stop the simulation
                        clearInterval(ecosystemGameTimerId);
                        ecosystemGameActive = false;
                        
                        // Add restart button event
                        document.getElementById('restart-ecosystem').addEventListener('click', function() {
                            resetEcosystem();
                        });
                    } else {
                        ecosystemStatus.innerHTML = `
                            <div class="text-yellow-400 font-bold mb-2">Ecosystem Imbalance</div>
                            <p>${statusMessage}</p>
                            <p class="mt-2 text-sm">Adjust your species composition to create balance.</p>
                        `;
                        ecosystemStatus.classList.add('bg-yellow-900', 'bg-opacity-20', 'border-yellow-800');
                        ecosystemStatus.classList.remove('bg-green-900', 'bg-opacity-20', 'border-green-800', 'bg-red-900', 'bg-opacity-20', 'border-red-800');
                    }
                }
            }
            
            // Update the population chart
            updateEcosystemChart();
        }
        
        // Function to create/update the ecosystem chart
        function updateEcosystemChart() {
            const chartCanvas = document.getElementById('ecosystem-chart');
            if (!chartCanvas) return;
            
            // Clear existing chart if any
            chartCanvas.innerHTML = '';
            
            // Create SVG for the chart
            const svg = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
            svg.setAttribute('width', '100%');
            svg.setAttribute('height', '100%');
            svg.setAttribute('viewBox', '0 0 300 150');
            
            // Calculate max value for scaling
            let maxValue = 1;
            for (let species in ecosystemPopulations) {
                const max = Math.max(...ecosystemPopulations[species]);
                if (max > maxValue) maxValue = max;
            }
            
            // Draw axes
            const axis = document.createElementNS('http://www.w3.org/2000/svg', 'path');
            axis.setAttribute('d', 'M 30 10 L 30 130 L 290 130');
            axis.setAttribute('stroke', '#6B7280');
            axis.setAttribute('stroke-width', '1');
            axis.setAttribute('fill', 'none');
            svg.appendChild(axis);
            
            // Add axis labels
            const yLabel = document.createElementNS('http://www.w3.org/2000/svg', 'text');
            yLabel.setAttribute('x', '10');
            yLabel.setAttribute('y', '75');
            yLabel.setAttribute('fill', '#9CA3AF');
            yLabel.setAttribute('font-size', '10');
            yLabel.setAttribute('transform', 'rotate(-90, 10, 75)');
            yLabel.textContent = 'Population';
            svg.appendChild(yLabel);
            
            const xLabel = document.createElementNS('http://www.w3.org/2000/svg', 'text');
            xLabel.setAttribute('x', '160');
            xLabel.setAttribute('y', '148');
            xLabel.setAttribute('fill', '#9CA3AF');
            xLabel.setAttribute('font-size', '10');
            xLabel.setAttribute('text-anchor', 'middle');
            xLabel.textContent = 'Days';
            svg.appendChild(xLabel);
            
            // Draw line for each species
            const colors = {
                'tree': '#10B981', // green
                'herbivore': '#FBBF24', // yellow
                'carnivore': '#EF4444', // red
                'apex': '#8B5CF6' // purple
            };
            
            for (let species in ecosystemPopulations) {
                const data = ecosystemPopulations[species];
                if (data.length <= 1) continue;
                
                // Create path for the line
                let pathD = '';
                data.forEach((value, index) => {
                    const x = 30 + (260 * index / (data.length - 1));
                    const y = 130 - (120 * value / maxValue);
                    
                    if (index === 0) {
                        pathD += `M ${x} ${y}`;
                    } else {
                        pathD += ` L ${x} ${y}`;
                    }
                });
                
                const path = document.createElementNS('http://www.w3.org/2000/svg', 'path');
                path.setAttribute('d', pathD);
                path.setAttribute('stroke', colors[species]);
                path.setAttribute('stroke-width', '2');
                path.setAttribute('fill', 'none');
                svg.appendChild(path);
                
                // Add a legend marker
                const legendX = 200 + (Object.keys(ecosystemPopulations).indexOf(species) * 20);
                const legendY = 15;
                
                const legendMarker = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
                legendMarker.setAttribute('x', legendX);
                legendMarker.setAttribute('y', legendY);
                legendMarker.setAttribute('width', '10');
                legendMarker.setAttribute('height', '3');
                legendMarker.setAttribute('fill', colors[species]);
                svg.appendChild(legendMarker);
                
                const legendText = document.createElementNS('http://www.w3.org/2000/svg', 'text');
                legendText.setAttribute('x', legendX - 5);
                legendText.setAttribute('y', legendY - 3);
                legendText.setAttribute('fill', colors[species]);
                legendText.setAttribute('font-size', '6');
                legendText.setAttribute('text-anchor', 'end');
                legendText.textContent = species.charAt(0).toUpperCase() + species.slice(1) + 's';
                svg.appendChild(legendText);
            }
            
            // Add to canvas
            chartCanvas.appendChild(svg);
        }
        
        // Function to reset ecosystem simulation
        function resetEcosystem() {
            // Stop any ongoing simulation
            if (ecosystemGameTimerId) {
                clearInterval(ecosystemGameTimerId);
            }
            
            // Reset variables
            ecosystemGameActive = false;
            ecosystemDays = 0;
            ecosystemSpecies = {'tree': 0, 'herbivore': 0, 'carnivore': 0, 'apex': 0};
            ecosystemPopulations = {
                'tree': [0],
                'herbivore': [0],
                'carnivore': [0],
                'apex': [0]
            };
            
            // Clear ecosystem canvas
            const ecosystemCanvas = document.getElementById('ecosystem-canvas');
            if (ecosystemCanvas) {
                // Remove all species icons
                document.querySelectorAll('.tree-icon, .herbivore-icon, .carnivore-icon, .apex-icon').forEach(icon => {
                    icon.remove();
                });
                
                // Show placeholder text
                const placeholder = document.querySelector('.ecosystem-placeholder');
                if (placeholder) {
                    placeholder.style.display = 'flex';
                }
            }
            
            // Reset status
            const ecosystemStatus = document.getElementById('ecosystem-status');
            if (ecosystemStatus) {
                ecosystemStatus.innerHTML = 'Ecosystem status: Ready to simulate';
                ecosystemStatus.className = 'mt-4 p-3 rounded bg-gray-900 text-gray-300 text-sm';
            }
            
            // Reset run button
            if (document.getElementById('run-ecosystem')) {
                document.getElementById('run-ecosystem').textContent = 'Run Simulation';
                document.getElementById('run-ecosystem').classList.remove('bg-red-600');
                document.getElementById('run-ecosystem').classList.add('bg-green-600');
            }
            
            // Update chart
            updateEcosystemChart();
        }
        
        // Initialize ecosystem species interaction
        if (document.querySelectorAll('.species-item')) {
            document.querySelectorAll('.species-item').forEach(item => {
                item.addEventListener('click', function() {
                    const species = this.getAttribute('data-species');
                    const placeholder = document.querySelector('.ecosystem-placeholder');
                    
                    if (placeholder) {
                        placeholder.style.display = 'none';
                    }
                    
                    // Add icon to the ecosystem
                    const ecosystemCanvas = document.getElementById('ecosystem-canvas');
                    if (ecosystemCanvas) {
                        const icon = document.createElement('div');
                        const xPos = Math.random() * 80 + 10; // 10-90% of width
                        const yPos = Math.random() * 80 + 10; // 10-90% of height
                        
                        let emoji = '🌳';
                        let color = 'bg-green-800';
                        
                        switch(species) {
                            case 'tree': 
                                emoji = '🌳'; 
                                color = 'bg-green-800';
                                break;
                            case 'herbivore': 
                                emoji = '🦋'; 
                                color = 'bg-yellow-800';
                                break;
                            case 'carnivore': 
                                emoji = '🦎'; 
                                color = 'bg-red-800';
                                break;
                            case 'apex': 
                                emoji = '🐆'; 
                                color = 'bg-purple-800';
                                break;
                        }
                        
                        icon.className = `absolute w-8 h-8 ${color} rounded-full flex items-center justify-center ${species}-icon`;
                        icon.style.left = `${xPos}%`;
                        icon.style.top = `${yPos}%`;
                        icon.innerHTML = `<span>${emoji}</span>`;
                        
                        ecosystemCanvas.appendChild(icon);
                        
                        // Update species count
                        ecosystemSpecies[species]++;
                        
                        // Also update the initial population count
                        if (ecosystemPopulations[species].length === 1 && ecosystemPopulations[species][0] === 0) {
                            ecosystemPopulations[species][0] = ecosystemSpecies[species];
                        } else {
                            const lastIndex = ecosystemPopulations[species].length - 1;
                            ecosystemPopulations[species][lastIndex] = ecosystemSpecies[species];
                        }
                        
                        // Update chart if simulation is not running
                        if (!ecosystemGameActive) {
                            updateEcosystemChart();
                        }
                    }
                });
            });
        }
        
        if (document.getElementById('run-ecosystem')) {
            document.getElementById('run-ecosystem').addEventListener('click', function() {
                // Check if we have any species
                const totalSpecies = Object.values(ecosystemSpecies).reduce((sum, count) => sum + count, 0);
                if (totalSpecies === 0) {
                    alert('Add some species to your ecosystem first!');
                    return;
                }
                
                // Toggle simulation
                if (ecosystemGameActive) {
                    // Stop simulation
                    clearInterval(ecosystemGameTimerId);
                    ecosystemGameActive = false;
                    this.textContent = 'Run Simulation';
                    this.classList.remove('bg-red-600');
                    this.classList.add('bg-green-600');
                } else {
                    // Start simulation
                    ecosystemGameActive = true;
                    this.textContent = 'Pause Simulation';
                    this.classList.remove('bg-green-600');
                    this.classList.add('bg-red-600');
                    
                    // Run the simulation
                    updateEcosystemSimulation(); // Initial update
                    ecosystemGameTimerId = setInterval(updateEcosystemSimulation, 1000);
                }
            });
        }
        
        if (document.getElementById('reset-ecosystem')) {
            document.getElementById('reset-ecosystem').addEventListener('click', resetEcosystem);
        }
        
        if (document.getElementById('balance-ecosystem')) {
            document.getElementById('balance-ecosystem').addEventListener('click', function() {
                // Auto-balance the ecosystem
                const ecosystemCanvas = document.getElementById('ecosystem-canvas');
                const placeholder = document.querySelector('.ecosystem-placeholder');
                
                // Remove all species icons
                document.querySelectorAll('.tree-icon, .herbivore-icon, .carnivore-icon, .apex-icon').forEach(icon => {
                    icon.remove();
                });
                
                // Reset species count
                ecosystemSpecies = {'tree': 0, 'herbivore': 0, 'carnivore': 0, 'apex': 0};
                
                // Hide placeholder text
                if (placeholder) {
                    placeholder.style.display = 'none';
                }
                
                // Add balanced distribution of species
                const species = ['tree', 'tree', 'tree', 'tree', 'tree', 'herbivore', 'herbivore', 'herbivore', 'carnivore', 'carnivore', 'apex'];
                const emojis = {'tree': '🌳', 'herbivore': '🦋', 'carnivore': '🦎', 'apex': '🐆'};
                const colors = {'tree': 'bg-green-800', 'herbivore': 'bg-yellow-800', 'carnivore': 'bg-red-800', 'apex': 'bg-purple-800'};
                
                species.forEach(type => {
                    const icon = document.createElement('div');
                    const xPos = Math.random() * 80 + 10;
                    const yPos = Math.random() * 80 + 10;
                    
                    icon.className = `absolute w-8 h-8 ${colors[type]} rounded-full flex items-center justify-center ${type}-icon`;
                    icon.style.left = `${xPos}%`;
                    icon.style.top = `${yPos}%`;
                    icon.innerHTML = `<span>${emojis[type]}</span>`;
                    
                    ecosystemCanvas.appendChild(icon);
                    
                    // Update species count
                    ecosystemSpecies[type]++;
                    
                    // Also update the initial population count
                    if (ecosystemPopulations[type].length === 1 && ecosystemPopulations[type][0] === 0) {
                        ecosystemPopulations[type][0] = ecosystemSpecies[type];
                    } else {
                        const lastIndex = ecosystemPopulations[type].length - 1;
                        ecosystemPopulations[type][lastIndex] = ecosystemSpecies[type];
                    }
                });
                
                // Update chart
                updateEcosystemChart();
                
                const ecosystemStatus = document.getElementById('ecosystem-status');
                ecosystemStatus.innerHTML = `
                    <div class="text-green-400 font-bold mb-2">Ecosystem automatically balanced</div>
                    <p>A sustainable ratio of producers and consumers has been created.</p>
                    <p class="mt-2 text-xs">Trees: 5 | Herbivores: 3 | Carnivores: 2 | Apex Predators: 1</p>
                `;
                ecosystemStatus.classList.add('bg-green-900', 'bg-opacity-20', 'border-green-800');
            });
        }
        
        //--------------------------------------------
        // Virus Outbreak Simulator Game Functionality
        //--------------------------------------------
        let virusGameActive = false;
        let virusGameTimerId = null;
        let virusDay = 0;
        let infectionsTotal = 0;
        let recoveredTotal = 0;
        let rValue = 2.5;
        let socialDistancingActive = false;
        let travelRestrictionsActive = false;
        let vaccineProgress = 0;
        let vaccineReady = false;
        let infectionsByRegion = {
            'north-america': 0,
            'south-america': 0,
            'europe': 0,
            'africa': 0,
            'asia': 10, // initial outbreak
            'australia': 0
        };
        
        function updateVirusSimulation() {
            virusDay++;
            document.getElementById('day-counter').textContent = `Day: ${virusDay}`;
            
            // Update R value based on interventions
            let currentR = rValue;
            if (socialDistancingActive) currentR *= 0.7;
            if (travelRestrictionsActive) currentR *= 0.8;
            if (vaccineReady) currentR *= 0.5;
            
            // Update infections based on R value
            const newInfections = Math.floor(infectionsTotal * (currentR / 10));
            infectionsTotal += newInfections;
            
            // Recoveries
            const newRecoveries = Math.floor(infectionsTotal * 0.05);
            recoveredTotal += newRecoveries;
            infectionsTotal -= newRecoveries;
            
            // Update vaccine progress
            if (vaccineProgress > 0 && !vaccineReady) {
                vaccineProgress++;
                if (vaccineProgress >= 20) {
                    vaccineReady = true;
                    addVirusLog(`Day ${virusDay}: Vaccine development complete! Starting mass vaccination.`);
                    document.getElementById('develop-vaccine').textContent = 'Vaccine Deployed';
                    document.getElementById('develop-vaccine').classList.remove('bg-blue-900');
                    document.getElementById('develop-vaccine').classList.add('bg-green-900');
                } else {
                    document.getElementById('develop-vaccine').textContent = `Developing: ${vaccineProgress}/20 days`;
                }
            }
            
            // Update infections by region based on travel
            const transmissionRate = document.getElementById('transmission-rate').value / 10;
            const regions = Object.keys(infectionsByRegion);
            
            regions.forEach(region => {
                if (infectionsByRegion[region] > 0) {
                    // Grow infections within the region
                    infectionsByRegion[region] *= (1 + transmissionRate * (currentR / rValue));
                    
                    // Spread to other regions if travel restrictions aren't active
                    if (!travelRestrictionsActive && Math.random() < 0.05) {
                        const targetRegion = regions[Math.floor(Math.random() * regions.length)];
                        if (targetRegion !== region) {
                            const spreadAmount = Math.floor(infectionsByRegion[region] * 0.01);
                            infectionsByRegion[targetRegion] += spreadAmount;
                            
                            // Add infection dots to map for newly infected regions
                            if (infectionsByRegion[targetRegion] === spreadAmount) {
                                addVirusLog(`Day ${virusDay}: Virus has spread to ${targetRegion.replace('-', ' ')}.`);
                                
                                // Add visual representation on the map
                                let x, y;
                                switch(targetRegion) {
                                    case 'north-america': x = 300; y = 150; break;
                                    case 'south-america': x = 350; y = 350; break;
                                    case 'europe': x = 450; y = 150; break;
                                    case 'africa': x = 450; y = 250; break;
                                    case 'asia': x = 600; y = 200; break;
                                    case 'australia': x = 700; y = 350; break;
                                }
                                
                                const map = document.querySelector('#virus-map svg');
                                if (map) {
                                    const dot = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
                                    dot.setAttribute('cx', x);
                                    dot.setAttribute('cy', y);
                                    dot.setAttribute('r', '5');
                                    dot.setAttribute('fill', '#DC2626');
                                    dot.classList.add('animate-pulse');
                                    map.appendChild(dot);
                                }
                            }
                        }
                    }
                }
            });
            
            // Random events based on mutation rate
            const mutationRate = document.getElementById('mutation-rate').value / 10;
            if (virusDay % 5 === 0 && Math.random() < mutationRate) {
                addVirusLog(`Day ${virusDay}: Virus mutation detected! Transmission characteristics changing.`);
                rValue *= 1.1;
                document.getElementById('r-value').textContent = rValue.toFixed(1);
            }
            
            // Log significant milestones
            if (infectionsTotal > 1000 && infectionsTotal < 2000) {
                addVirusLog(`Day ${virusDay}: Infections exceed 1,000 cases globally.`);
            } else if (infectionsTotal > 10000 && infectionsTotal < 15000) {
                addVirusLog(`Day ${virusDay}: Infections exceed 10,000 cases. WHO declares global health emergency.`);
            } else if (infectionsTotal > 100000 && infectionsTotal < 150000) {
                addVirusLog(`Day ${virusDay}: Infections exceed 100,000 cases. International cooperation intensifies.`);
            }
            
            // Adjust difficulty with severity
            const severity = document.getElementById('severity').value / 10;
            if (severity > 0.5 && Math.random() < severity * 0.1) {
                // Add complications
                if (Math.random() < 0.5) {
                    addVirusLog(`Day ${virusDay}: New severe symptoms emerging, increasing healthcare burden.`);
                } else {
                    addVirusLog(`Day ${virusDay}: Virus showing resistance to standard treatments.`);
                }
            }
            
            // Update stats display
            updateVirusStats();
            
            // End conditions
            if (virusDay >= 100 || (vaccineReady && infectionsTotal < 100)) {
                clearInterval(virusGameTimerId);
                virusGameActive = false;
                document.getElementById('start-outbreak').textContent = 'Start New Outbreak';
                document.getElementById('start-outbreak').disabled = false;
                
                // Final report
                const finalInfected = Math.floor(infectionsTotal);
                const finalRecovered = Math.floor(recoveredTotal);
                const totalCases = finalInfected + finalRecovered;
                
                let outcome;
                if (finalInfected < 1000) {
                    outcome = "Excellent containment! The outbreak was successfully managed with minimal impact.";
                } else if (finalInfected < 10000) {
                    outcome = "Good response. The outbreak was contained before becoming a major pandemic.";
                } else if (finalInfected < 100000) {
                    outcome = "Moderate outcome. The pandemic had significant impact but was eventually controlled.";
                } else {
                    outcome = "Severe pandemic. The outbreak had widespread global impact.";
                }
                
                addVirusLog(`Simulation complete. ${outcome} Final results: ${finalInfected.toLocaleString()} active cases, ${finalRecovered.toLocaleString()} recovered, ${totalCases.toLocaleString()} total cases.`);
            }
        }
        
        function updateVirusStats() {
            document.getElementById('infection-count').textContent = Math.floor(infectionsTotal).toLocaleString();
            document.getElementById('recovery-count').textContent = Math.floor(recoveredTotal).toLocaleString();
            document.getElementById('r-value').textContent = rValue.toFixed(1);
        }
        
        function addVirusLog(message) {
            const log = document.getElementById('virus-status-log');
            const entry = document.createElement('p');
            entry.className = 'mb-1';
            entry.textContent = message;
            log.prepend(entry);
            
            // Keep log from getting too long
            const entries = log.querySelectorAll('p');
            if (entries.length > 10) {
                entries[entries.length - 1].remove();
            }
        }
        
        function resetVirusSimulation() {
            // Reset all variables
            virusGameActive = false;
            virusDay = 0;
            infectionsTotal = 0;
            recoveredTotal = 0;
            rValue = 2.5;
            socialDistancingActive = false;
            travelRestrictionsActive = false;
            vaccineProgress = 0;
            vaccineReady = false;
            infectionsByRegion = {
                'north-america': 0,
                'south-america': 0,
                'europe': 0,
                'africa': 0,
                'asia': 0,
                'australia': 0
            };
            
            // Reset UI
            document.getElementById('day-counter').textContent = 'Day: 0';
            document.getElementById('infection-count').textContent = '0';
            document.getElementById('recovery-count').textContent = '0';
            document.getElementById('r-value').textContent = '2.5';
            
            // Clear infection dots from map
            const map = document.querySelector('#virus-map svg');
            if (map) {
                const dots = map.querySelectorAll('circle:not(#outbreak-start)');
                dots.forEach(dot => dot.remove());
            }
            
            // Reset intervention buttons
            if (document.getElementById('social-distancing')) {
                document.getElementById('social-distancing').classList.remove('bg-green-900');
                document.getElementById('social-distancing').classList.add('bg-blue-900');
                document.getElementById('social-distancing').textContent = 'Implement Social Distancing';
            }
            
            if (document.getElementById('travel-restrictions')) {
                document.getElementById('travel-restrictions').classList.remove('bg-green-900');
                document.getElementById('travel-restrictions').classList.add('bg-blue-900');
                document.getElementById('travel-restrictions').textContent = 'Impose Travel Restrictions';
            }
            
            if (document.getElementById('develop-vaccine')) {
                document.getElementById('develop-vaccine').classList.remove('bg-green-900');
                document.getElementById('develop-vaccine').classList.add('bg-blue-900');
                document.getElementById('develop-vaccine').textContent = 'Develop Vaccine (20 days)';
            }
            
            // Clear log
            const log = document.getElementById('virus-status-log');
            if (log) {
                log.innerHTML = '<p class="mb-1">System ready. Configure virus parameters and press Start Outbreak to begin.</p>';
            }
            
            // Enable start button
            if (document.getElementById('start-outbreak')) {
                document.getElementById('start-outbreak').textContent = 'Start Outbreak';
                document.getElementById('start-outbreak').disabled = false;
            }
        }
        
        if (document.getElementById('start-outbreak')) {
            document.getElementById('start-outbreak').addEventListener('click', function() {
                if (virusGameActive) {
                    return; // Already running
                }
                
                // Reset simulation if it was previously run
                resetVirusSimulation();
                
                // Start with initial outbreak in Asia
                infectionsTotal = 10;
                infectionsByRegion.asia = 10;
                
                // Get virus parameters
                const transmissionRate = document.getElementById('transmission-rate').value;
                const mutationRate = document.getElementById('mutation-rate').value;
                const severity = document.getElementById('severity').value;
                
                // Calculate R value based on transmission
                rValue = (transmissionRate / 2);
                document.getElementById('r-value').textContent = rValue.toFixed(1);
                
                // Start simulation
                updateVirusStats();
                addVirusLog('Day 0: Outbreak detected in Eastern Asia. 10 initial cases reported.');
                
                // Start simulation interval
                virusGameActive = true;
                this.textContent = 'Simulation Running...';
                this.disabled = true;
                
                if (virusGameTimerId) clearInterval(virusGameTimerId);
                virusGameTimerId = setInterval(updateVirusSimulation, 1000);
            });
        }
        
        if (document.getElementById('social-distancing')) {
            document.getElementById('social-distancing').addEventListener('click', function() {
                if (!virusGameActive) {
                    alert('Start the outbreak simulation first!');
                    return;
                }
                
                socialDistancingActive = !socialDistancingActive;
                
                if (socialDistancingActive) {
                    this.classList.remove('bg-blue-900');
                    this.classList.add('bg-green-900');
                    this.textContent = 'Social Distancing Active';
                    
                    addVirusLog(`Day ${virusDay}: Social distancing measures implemented. Transmission rate reduced.`);
                } else {
                    this.classList.remove('bg-green-900');
                    this.classList.add('bg-blue-900');
                    this.textContent = 'Implement Social Distancing';
                    
                    addVirusLog(`Day ${virusDay}: Social distancing measures relaxed. Transmission rate increased.`);
                }
            });
        }
        
        if (document.getElementById('travel-restrictions')) {
            document.getElementById('travel-restrictions').addEventListener('click', function() {
                if (!virusGameActive) {
                    alert('Start the outbreak simulation first!');
                    return;
                }
                
                travelRestrictionsActive = !travelRestrictionsActive;
                
                if (travelRestrictionsActive) {
                    this.classList.remove('bg-blue-900');
                    this.classList.add('bg-green-900');
                    this.textContent = 'Travel Restrictions Active';
                    
                    addVirusLog(`Day ${virusDay}: Travel restrictions implemented. Cross-border transmission reduced.`);
                } else {
                    this.classList.remove('bg-green-900');
                    this.classList.add('bg-blue-900');
                    this.textContent = 'Impose Travel Restrictions';
                    
                    addVirusLog(`Day ${virusDay}: Travel restrictions lifted. Cross-border transmission increased.`);
                }
            });
        }
        
        if (document.getElementById('develop-vaccine')) {
            document.getElementById('develop-vaccine').addEventListener('click', function() {
                if (!virusGameActive) {
                    alert('Start the outbreak simulation first!');
                    return;
                }
                
                if (vaccineProgress === 0) {
                    vaccineProgress = 1;
                    addVirusLog(`Day ${virusDay}: Vaccine development started. Estimated completion in 20 days.`);
                    
                    // Update button
                    this.textContent = 'Developing: 1/20 days';
                }
            });
        }
        
        //--------------------------------------------
        // Evolution Arena Game Functionality
        //--------------------------------------------
        let evolutionGameActive = false;
        let evolutionGameTimerId = null;
        let traitPoints = 10;
        let traitValues = {
            'heat': 0,
            'cold': 0,
            'water': 0,
            'pressure': 0,
            'acid': 0
        };
        let currentGeneration = 0;
        let survivalChance = 0;
        
        // Initialize trait buttons
        document.querySelectorAll('.trait-btn').forEach(button => {
            button.addEventListener('click', function() {
                const trait = this.getAttribute('data-trait');
                const action = this.getAttribute('data-action');
                
                if (action === 'increase' && traitPoints > 0) {
                    traitValues[trait]++;
                    traitPoints--;
                    document.getElementById(`${trait}-value`).textContent = traitValues[trait];
                    
                    // Show visual trait on organism
                    document.getElementById(`${trait}-feature`).classList.remove('hidden');
                    
                } else if (action === 'decrease' && traitValues[trait] > 0) {
                    traitValues[trait]--;
                    traitPoints++;
                    document.getElementById(`${trait}-value`).textContent = traitValues[trait];
                    
                    // Hide visual trait if zero
                    if (traitValues[trait] === 0) {
                        document.getElementById(`${trait}-feature`).classList.add('hidden');
                    }
                }
                
                // Update available points
                document.getElementById('trait-points').textContent = traitPoints;
                
                // Calculate current survival chance
                calculateSurvivalChance();
            });
        });
        
        function calculateSurvivalChance() {
            const environment = document.getElementById('environment-select').value;
            let score = 0;
            
            switch(environment) {
                case 'desert':
                    // Desert needs heat resistance and water conservation
                    score = (traitValues.heat * 2) + (traitValues.water * 3);
                    break;
                    
                case 'arctic':
                    // Arctic needs cold resistance
                    score = (traitValues.cold * 4) + (traitValues.water * 1);
                    break;
                    
                case 'ocean':
                    // Ocean needs pressure tolerance and cold resistance
                    score = (traitValues.pressure * 3) + (traitValues.cold * 2);
                    break;
                    
                case 'volcanic':
                    // Volcanic needs heat resistance and acid resistance
                    score = (traitValues.heat * 2) + (traitValues.acid * 3);
                    break;
            }
            
            // Calculate survival percentage (max score would be 5 points in two categories = 25)
            survivalChance = Math.min(Math.round((score / 25) * 100), 100);
            document.getElementById('survival-progress').style.width = `${survivalChance}%`;
        }
        
        function runEvolutionSimulation() {
            currentGeneration++;
            document.getElementById('generation-counter').textContent = `Generation: ${currentGeneration}`;
            
            const environment = document.getElementById('environment-select').value;
            
            // Each generation has a chance to mutate and improve traits
            const randomTrait = ['heat', 'cold', 'water', 'pressure', 'acid'][Math.floor(Math.random() * 5)];
            
            // Survival check
            if (Math.random() * 100 < survivalChance) {
                // Organism survived, possible beneficial mutation
                if (Math.random() < 0.3) { // 30% chance of beneficial mutation
                    // Only increase if it would be useful in this environment
                    let useful = false;
                    
                    switch(environment) {
                        case 'desert':
                            useful = (randomTrait === 'heat' || randomTrait === 'water');
                            break;
                        case 'arctic':
                            useful = (randomTrait === 'cold' || randomTrait === 'water');
                            break;
                        case 'ocean':
                            useful = (randomTrait === 'pressure' || randomTrait === 'cold');
                            break;
                        case 'volcanic':
                            useful = (randomTrait === 'heat' || randomTrait === 'acid');
                            break;
                    }
                    
                    if (useful && traitValues[randomTrait] < 5) {
                        traitValues[randomTrait]++;
                        document.getElementById(`${randomTrait}-value`).textContent = traitValues[randomTrait];
                        document.getElementById(`${randomTrait}-feature`).classList.remove('hidden');
                        
                        addEvolutionLog(`Generation ${currentGeneration}: Beneficial mutation! ${randomTrait} resistance increased.`);
                    } else {
                        addEvolutionLog(`Generation ${currentGeneration}: Organism survived without changes.`);
                    }
                } else {
                    addEvolutionLog(`Generation ${currentGeneration}: Organism survived.`);
                }
            } else {
                // Organism struggled, but adapted
                addEvolutionLog(`Generation ${currentGeneration}: Organism struggled to survive.`);
                
                // Determine which trait would be most beneficial
                let bestTrait = '';
                
                switch(environment) {
                    case 'desert':
                        bestTrait = traitValues.heat < traitValues.water ? 'heat' : 'water';
                        break;
                    case 'arctic':
                        bestTrait = 'cold';
                        break;
                    case 'ocean':
                        bestTrait = traitValues.pressure < traitValues.cold ? 'pressure' : 'cold';
                        break;
                    case 'volcanic':
                        bestTrait = traitValues.heat < traitValues.acid ? 'heat' : 'acid';
                        break;
                }
                
                // 50% chance to develop this trait
                if (Math.random() < 0.5 && traitValues[bestTrait] < 5) {
                    traitValues[bestTrait]++;
                    document.getElementById(`${bestTrait}-value`).textContent = traitValues[bestTrait];
                    document.getElementById(`${bestTrait}-feature`).classList.remove('hidden');
                    
                    addEvolutionLog(`Generation ${currentGeneration}: Adaptation! ${bestTrait} resistance developed.`);
                }
            }
            
            // Recalculate survival chance
            calculateSurvivalChance();
            
            // Visually update the organism (make it pulse)
            const organism = document.getElementById('organism');
            if (organism) {
                organism.classList.add('animate-pulse');
                setTimeout(() => {
                    organism.classList.remove('animate-pulse');
                }, 500);
            }
            
            // End condition
            if (currentGeneration >= 10 || survivalChance >= 95) {
                clearInterval(evolutionGameTimerId);
                evolutionGameActive = false;
                
                if (survivalChance >= 95) {
                    addEvolutionLog(`Evolution complete! Your organism has successfully adapted to the ${environment} environment.`);
                } else {
                    addEvolutionLog(`Simulation ended after 10 generations. Final survival chance: ${survivalChance}%.`);
                }
                
                document.getElementById('run-evolution').textContent = 'Run Evolution';
                document.getElementById('run-evolution').disabled = false;
                
                // Show results
                const evolutionLog = document.getElementById('evolution-log');
                evolutionLog.innerHTML += `
                    <div class="mt-4 p-2 ${survivalChance >= 75 ? 'bg-green-900 bg-opacity-20 border-green-800' : 'bg-yellow-900 bg-opacity-20 border-yellow-800'} border rounded">
                        <p class="font-medium ${survivalChance >= 75 ? 'text-green-300' : 'text-yellow-300'}">Final Results:</p>
                        <p>Environment: ${environment.charAt(0).toUpperCase() + environment.slice(1)}</p>
                        <p>Generations: ${currentGeneration}</p>
                        <p>Survival Rate: ${survivalChance}%</p>
                        <div class="mt-2 grid grid-cols-5 gap-2 text-xs text-center">
                            <div>Heat: ${traitValues.heat}</div>
                            <div>Cold: ${traitValues.cold}</div>
                            <div>Water: ${traitValues.water}</div>
                            <div>Pressure: ${traitValues.pressure}</div>
                            <div>Acid: ${traitValues.acid}</div>
                        </div>
                    </div>
                `;
            }
        }
        
        function resetEvolutionSimulation() {
            // Stop any ongoing simulation
            if (evolutionGameTimerId) {
                clearInterval(evolutionGameTimerId);
            }
            
            // Reset variables
            evolutionGameActive = false;
            traitPoints = 10;
            traitValues = {
                'heat': 0,
                'cold': 0,
                'water': 0,
                'pressure': 0,
                'acid': 0
            };
            currentGeneration = 0;
            survivalChance = 0;
            
            // Reset UI
            document.getElementById('trait-points').textContent = traitPoints;
            document.querySelectorAll('.trait-value').forEach(val => {
                val.textContent = '0';
            });
            document.querySelectorAll('#heat-feature, #cold-feature, #water-feature, #pressure-feature, #acid-feature').forEach(feature => {
                feature.classList.add('hidden');
            });
            document.getElementById('generation-counter').textContent = 'Generation: 0';
            document.getElementById('survival-progress').style.width = '0%';
            document.getElementById('evolution-log').innerHTML = '<p class="mb-1">Welcome to Evolution Arena. Select an environment and assign traits to begin.</p>';
            
            // Enable run button
            document.getElementById('run-evolution').textContent = 'Run Evolution';
            document.getElementById('run-evolution').disabled = false;
        }
        
        function addEvolutionLog(message) {
            const log = document.getElementById('evolution-log');
            if (!log) return;
            
            const entry = document.createElement('p');
            entry.className = 'mb-1';
            entry.textContent = message;
            log.prepend(entry);
            
            // Keep log from getting too long
            const entries = log.querySelectorAll('p');
            if (entries.length > 8) {
                entries[entries.length - 1].remove();
            }
        }
        
        if (document.getElementById('environment-select')) {
            document.getElementById('environment-select').addEventListener('change', function() {
                calculateSurvivalChance();
                
                // Log the environment change
                const environment = this.value;
                addEvolutionLog(`Environment changed to ${environment}. Adapt your organism to survive.`);
                
                // Change the organism canvas background
                const canvas = document.getElementById('organism-canvas');
                
                // Remove all environment classes
                canvas.classList.remove('bg-yellow-900', 'bg-blue-900', 'bg-indigo-900', 'bg-red-900');
                
                // Add the right environment class
                switch(environment) {
                    case 'desert':
                        canvas.classList.add('bg-yellow-900');
                        break;
                    case 'arctic':
                        canvas.classList.add('bg-blue-900');
                        break;
                    case 'ocean':
                        canvas.classList.add('bg-indigo-900');
                        break;
                    case 'volcanic':
                        canvas.classList.add('bg-red-900');
                        break;
                }
            });
        }
        
        if (document.getElementById('run-evolution')) {
            document.getElementById('run-evolution').addEventListener('click', function() {
                if (evolutionGameActive) {
                    return; // Already running
                }
                
                // Check if any traits are allocated
                const totalTraits = Object.values(traitValues).reduce((sum, val) => sum + val, 0);
                if (totalTraits === 0) {
                    alert('Assign some traits to your organism first!');
                    return;
                }
                
                // Reset generation counter
                currentGeneration = 0;
                document.getElementById('generation-counter').textContent = `Generation: ${currentGeneration}`;
                
                // Log start
                const environment = document.getElementById('environment-select').value;
                addEvolutionLog(`Evolution simulation started in ${environment} environment.`);
                addEvolutionLog(`Initial survival chance: ${survivalChance}%`);
                
                // Start evolution simulation
                evolutionGameActive = true;
                this.textContent = 'Simulation Running...';
                this.disabled = true;
                
                if (evolutionGameTimerId) clearInterval(evolutionGameTimerId);
                evolutionGameTimerId = setInterval(runEvolutionSimulation, 1500);
            });
        }
        
        if (document.getElementById('reset-evolution')) {
            document.getElementById('reset-evolution').addEventListener('click', resetEvolutionSimulation);
        }
    </script>
</body>
</html>
