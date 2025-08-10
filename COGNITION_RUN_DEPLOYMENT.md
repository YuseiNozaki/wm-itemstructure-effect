# Cognition.run Deployment Instructions

This project is designed for deployment on cognition.run platform. The experiment implements a working memory and visual search task using jsPsych v7.

## Files for Deployment

### 1. JavaScript Code
**File:** `index.html` (JavaScript section)
- Contains the complete experiment logic within a specific `<script>` tag
- Look for the `<script>` tag with the comment `<!-- Experiment Logic -->` above it
- Copy only the JavaScript code within this `<script>` tag (excluding the script tags themselves)
- Includes dynamic DOM element creation for cognition.run compatibility
- Ready to extract and paste into cognition.run JavaScript section

### 2. CSS Styles  
**File:** `styles.css`
- Contains all styling required for the experiment
- Should be uploaded as a separate CSS file in cognition.run
- Includes styles for memory grid, search window, and visual elements

## Deployment Steps

1. **Upload CSS File:**
   - Upload `styles.css` to cognition.run as a separate CSS file
   - The CSS will be automatically linked to your experiment

2. **Extract and Copy JavaScript Code:**
   - Open `index.html` in a text editor
   - Copy the entire contents between the `<script>` tags (excluding the script tags themselves)
   - Paste into the JavaScript section of cognition.run

3. **Required External Libraries:**
   Add these external libraries in cognition.run's library settings:
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

4. **Experiment Configuration:**
   - Set experiment to run in fullscreen mode
   - Ensure participant consent and data collection settings are configured
   - Test all three viewing conditions (fullscreen, window, scroll) before deployment

## Key Features for Cognition.run Deployment

1. **Dynamic DOM Creation:** All required HTML elements (`div`, `canvas`) are created dynamically via JavaScript
2. **CSS Separation:** All styles are contained in external `styles.css` file
3. **jsPsych v7 Compatibility:** Updated to use modern jsPsych v7 API
4. **Responsive Design:** Adapts to different screen sizes and resolutions
5. **Data Collection:** Comprehensive data output in JSON format at experiment completion

## Experiment Specifications

### Technical Requirements
- **Duration:** Approximately 15-20 minutes
- **Screen Resolution:** Minimum 1024x768, fullscreen recommended  
- **Browser Compatibility:** Modern browsers (Chrome, Firefox, Safari, Edge)
- **Participant Input:** Mouse/trackpad for object selection and window manipulation

### Experimental Conditions
- **Viewing Conditions:** 3 types (fullscreen, window drag, scroll drag)
- **Object Layout:** 2 types (structured grid, unstructured random)
- **Memory Load:** 2 conditions (with/without working memory task)
- **Total Trials:** 120 main trials + practice trials

### Memory Load Counterbalancing
The experiment implements automatic counterbalancing for memory load conditions using cognition.run's CONDITION variable:
- **CONDITION = 0, 2, 4... (even values):** Without memory → With memory
- **CONDITION = 1, 3, 5... (odd values):** With memory → Without memory
- **Local testing:** Random assignment when CONDITION variable is unavailable

This ensures balanced assignment across participants while maintaining local testing capability.

### Data Output
The experiment collects:
- Reaction times and accuracy for visual search tasks
- Mouse movement trajectories and total movement distance
- Working memory task performance (when applicable)
- Demographic information (age, gender)
- Trial-by-trial condition information
- Counterbalancing assignment data (CONDITION value, block order, assignment source)

## Verification and Testing

### Pre-deployment Checklist
- [ ] All jsPsych v7 plugins load correctly
- [ ] CSS file uploads and applies properly
- [ ] Fullscreen functionality works on target devices
- [ ] All three viewing conditions (fullscreen, window, scroll) function correctly
- [ ] Memory task displays and records responses accurately
- [ ] Data collection outputs complete JSON at experiment end
- [ ] Practice trials allow repetition before main experiment
- [ ] Demographic survey collects required information

### Local Testing Before Deployment
1. Open `index.html` in a browser
2. Complete the full experiment workflow:
   - Welcome screen and demographics
   - Practice trials (test all viewing conditions)
   - Main experiment blocks (with and without memory)
   - Data output verification
3. Test on multiple browsers and screen sizes
4. Verify all interactions work correctly (clicking, dragging, scrolling)

### Common Deployment Issues
- **Fullscreen Problems:** Ensure cognition.run allows fullscreen API access
- **Library Loading:** Verify all jsPsych plugins load in correct order
- **CSS Conflicts:** Check that custom styles don't conflict with cognition.run defaults
- **Data Saving:** Confirm cognition.run data collection integration works properly

### Troubleshooting
- If objects don't display: Check canvas creation and drawing functions
- If clicking doesn't work: Verify event listeners and collision detection
- If memory task fails: Check grid creation and selection tracking
- If drag operations fail: Ensure mouse event handling is properly configured

## Platform-Specific Notes

### Cognition.run Configuration
- Set experiment type to "Custom JavaScript"
- Enable fullscreen mode in experiment settings
- Configure data export to include all trial data
- Set appropriate time limits for experiment completion
- **Configure CONDITION variable for counterbalancing:** Assign sequential values (0,1,2,3...) to ensure balanced memory load assignment across participants
- Consider adding progress indicators for participant experience

### Performance Optimization
- The experiment is optimized for smooth performance with 25 objects per trial
- Canvas operations are efficient for real-time mouse tracking
- Memory usage is minimal with dynamic element creation/destruction