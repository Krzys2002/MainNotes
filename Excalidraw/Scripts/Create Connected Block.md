/*
```js
*/
// 1. Script Settings & Configuration
if(!ea.verifyMinimumPluginVersion || !ea.verifyMinimumPluginVersion("1.9.0")) {
  new Notice("This script requires a newer version of Excalidraw.");
  return;
}

let settings = ea.getScriptSettings();

// Default Settings
if (!settings["Block Width"]) {
  settings = {
    "Block Width": { value: 100, description: "Standard width for functional blocks" },
    "Block Height": { value: 60, description: "Standard height for functional blocks" },
    "Connection Gap": { value: 100, description: "Distance between connected blocks" },
    "Sum Block Size": { value: 40, description: "Diameter of the Sum circle" },
    "Style Template": { 
        value: "Simulink Light", 
        valueset: ["Simulink Light", "Simulink Dark"],
        description: "Choose a visual theme for the blocks"
    }
  };
  await ea.setScriptSettings(settings);
}

// Map settings to variables
const BLOCK_WIDTH = settings["Block Width"].value;
const BLOCK_HEIGHT = settings["Block Height"].value;
const GAP = settings["Connection Gap"].value;
const SUM_SIZE = settings["Sum Block Size"].value;
const THEME = settings["Style Template"].value;

// Define Style based on Template
const isDark = THEME === "Simulink Dark";
const STROKE_COLOR = isDark ? "#ffffff" : "#1e1e1e";
const BG_COLOR = isDark ? "#2d2d2d" : "#ffffff";

// 2. Initialization
ea.clear();
let selectedElements = ea.getViewSelectedElements();
let selectedEl = selectedElements.length > 0 ? selectedElements[0] : null;

let startX = 0, startY = 0, selectionWidth = 0, selectionHeight = 0;

if (selectedEl) {
  ea.copyViewElementsToEAforEditing([selectedEl]);
  let bb = ea.getBoundingBox([selectedEl]);
  startX = bb.topX;
  startY = bb.topY;
  selectionWidth = bb.width;
  selectionHeight = bb.height;
}

// 3. UI Selection
let blockTypes = ["Transfer Function", "Sum Block", "Integral (1/s)", "Derivative (s)", "Gain"];
let blockChoice = await utils.suggester(blockTypes, blockTypes, "Select Block Type");
if (!blockChoice) return;

let pathModes = ["Forward Path", "Feedback Path"];
let pathChoice = await utils.suggester(pathModes, pathModes, "Select Path Direction");
if (!pathChoice) return;

// 4. Apply Visual Style
ea.style.backgroundColor = BG_COLOR;
ea.style.strokeColor = STROKE_COLOR;
ea.style.fillStyle = "solid";
ea.style.strokeSharpness = "sharp";
ea.style.roundness = null; 
ea.style.strokeWidth = 1;

// 5. Position Calculation
let targetX = startX + selectionWidth + GAP;
let targetY = startY + (selectionHeight / 2) - (BLOCK_HEIGHT / 2);

if (pathChoice === "Feedback Path") {
    targetX = startX - GAP - BLOCK_WIDTH;
    targetY = startY + selectionHeight + (GAP / 2);
}

if (!selectedEl) {
    targetX = 0; targetY = 0;
}

let blockId;
let idsToGroup = [];

// 6. Block Creation Logic
if (blockChoice === "Transfer Function") {
    let math = await utils.inputPrompt("LaTeX Math", "", "\\frac{1}{s+1}");
    if (!math) return;
    
    let texData = await ea.tex2dataURL(math);
    let tw = texData.size.width;
    let th = texData.size.height;
    
    let rectW = Math.max(BLOCK_WIDTH, tw + 40);
    let rectH = Math.max(BLOCK_HEIGHT, th + 20);
    
    let containerId = ea.addRect(targetX, targetY, rectW, rectH);
    let rectEl = ea.getElement(containerId);
    
    let texId = await ea.addLaTex(
        rectEl.x + (rectW / 2) - (tw / 2), 
        rectEl.y + (rectH / 2) - (th / 2), 
        math
    );
    
    idsToGroup.push(containerId, texId);
    blockId = containerId;

} else if (blockChoice === "Sum Block") {
    let signs = await utils.inputPrompt("Signs (Left, Top, Bottom)", "e.g. ++-", "++-");
    if (!signs) return;

    let circleY = targetY + (BLOCK_HEIGHT / 2) - (SUM_SIZE / 2);
    let containerId = ea.addEllipse(targetX, circleY, SUM_SIZE, SUM_SIZE);
    let circleEl = ea.getElement(containerId);
    idsToGroup.push(containerId);

    let signArr = signs.split("");
    ea.style.fontSize = 16;

    for (let i = 0; i < signArr.length; i++) {
        if (i > 2) break;
        let char = signArr[i];
        let m = ea.measureText(char);
        let sX = 0, sY = 0;

        if (i === 0) { // Left
            sX = circleEl.x + 2;
            sY = circleEl.y + (SUM_SIZE / 2) - (m.height / 2);
        } else if (i === 1) { // Top
            sX = circleEl.x + (SUM_SIZE / 2) - (m.width / 2);
            sY = circleEl.y + 1;
        } else if (i === 2) { // Bottom
            sX = circleEl.x + (SUM_SIZE / 2) - (m.width / 2);
            sY = circleEl.y + SUM_SIZE - m.height - 1;
        }
        let sId = ea.addText(sX, sY, char);
        idsToGroup.push(sId);
    }
    blockId = containerId;

} else {
    // Integral, Derivative, or Gain
    let label = blockChoice.includes("Integral") ? "1/s" : (blockChoice.includes("Derivative") ? "s" : "K");
    if (blockChoice === "Gain") {
        label = await utils.inputPrompt("Gain value", "", "K") || "K";
    }

    let m = ea.measureText(label);
    let rectW = Math.max(BLOCK_WIDTH, m.width + 40);
    let rectH = BLOCK_HEIGHT;

    let containerId = (blockChoice === "Gain") 
        ? ea.addDiamond(targetX, targetY, rectW, rectH)
        : ea.addRect(targetX, targetY, rectW, rectH);
    
    let rectEl = ea.getElement(containerId);
    let txtId = ea.addText(
        rectEl.x + (rectW / 2) - (m.width / 2), 
        rectEl.y + (rectH / 2) - (m.height / 2), 
        label
    );
    
    idsToGroup.push(containerId, txtId);
    blockId = containerId;
}

ea.addToGroup(idsToGroup);

// 7. Connection Logic
if (selectedEl) {
    if (pathChoice === "Forward Path") {
        ea.connectObjects(selectedEl.id, null, blockId, null, {
            startFixedPoint: [1, 0.5],
            endFixedPoint: [0, 0.5],
            endArrowHead: "triangle"
        });
    } else {
        // Feedback loop orthogonal logic
        let blockEl = ea.getElement(blockId);
        let sourceCX = startX + selectionWidth;
        let sourceCY = startY + selectionHeight / 2;
        let targetCX = targetX + blockEl.width;
        let targetCY = targetY + blockEl.height / 2;
        let midX = sourceCX + (GAP / 2);
        
        ea.addArrow([
            [sourceCX, sourceCY],
            [midX, sourceCY],
            [midX, targetCY],
            [targetCX, targetCY]
        ], {
            endArrowHead: "triangle",
            startObjectId: selectedEl.id,
            endObjectId: blockId
        });
    }
}

// 8. Commit
await ea.addElementsToView(false, false);

