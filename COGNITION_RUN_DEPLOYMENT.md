# Cognition.run Deployment Instructions

This project has been restructured for deployment on cognition.run. The program functionality remains identical to the original.

## Files for Deployment

### 1. JavaScript Code
**File:** `cognition-run-script.js`
- Contains the complete experiment logic
- Includes DOM element creation at the beginning
- Ready to copy-paste into cognition.run JavaScript section

### 2. CSS Styles
**File:** `styles.css`
- Contains all the styling required for the experiment
- Should be uploaded as a separate CSS file in cognition.run

## Deployment Steps

1. **Upload CSS File:**
   - Upload `styles.css` to cognition.run as a separate CSS file
   - The CSS will be automatically linked

2. **Copy JavaScript Code:**
   - Open `cognition-run-script.js`
   - Copy the entire contents
   - Paste into the JavaScript section of cognition.run

3. **Required External Libraries:**
   The experiment requires these external libraries (include as script tags in cognition.run):
   ```html
   <script src="https://unpkg.com/jspsych@7"></script>
   <script src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1"></script>
   <script src="https://unpkg.com/@jspsych/plugin-survey-text@1"></script>
   <script src="https://unpkg.com/@jspsych/plugin-preload@1"></script>
   <script src="https://unpkg.com/@jspsych/plugin-instructions@1"></script>
   <script src="https://unpkg.com/@jspsych/plugin-canvas-keyboard-response@1"></script>
   <script src="https://unpkg.com/@jspsych/plugin-survey-multi-choice@1"></script>
   <link href="https://unpkg.com/jspsych@7/css/jspsych.css" rel="stylesheet" type="text/css" />
   ```

## Key Changes Made

1. **HTML Elements:** All HTML elements (`div`, `canvas`) are now created dynamically via JavaScript
2. **CSS Separation:** All styles moved to external `styles.css` file

## Verification

The modified version maintains 100% identical functionality to the original:
- All visual search conditions work the same way
- Memory tasks function identically  
- User interface and interactions are unchanged
- Data collection and experiment flow remain the same

## Local Testing

To test locally:
1. Open `index.html` in a browser
2. The experiment should run exactly as before
3. All DOM elements are created and styled correctly

The restructured files ensure compatibility with cognition.run's deployment requirements while preserving all original functionality.