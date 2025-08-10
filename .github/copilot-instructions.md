# Working Memory and Item Structure Effect - Psychology Experiment

This is a jsPsych v7-based psychology experiment that studies working memory effects on visual search tasks. The experiment runs entirely in the browser and measures reaction times, accuracy, and mouse movement patterns across different viewing conditions and memory loads.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Bootstrap and Setup
- No build system required - this is a pure HTML/CSS/JavaScript application
- **CRITICAL**: Start a local web server to test: `python3 -m http.server 8000` in project root
- **NEVER CANCEL**: Web server runs indefinitely. Use Ctrl+C to stop when done
- Navigate to `http://localhost:8000` to run the main experiment
- Navigate to `http://localhost:8000/tests/` to access individual test files

### Dependencies and CDN Resources
- **External Dependencies**: All loaded via CDN from unpkg.com
  - `https://unpkg.com/jspsych@7` - Core jsPsych framework
  - `https://unpkg.com/@jspsych/plugin-html-keyboard-response@1`
  - `https://unpkg.com/@jspsych/plugin-survey-text@1`
  - `https://unpkg.com/@jspsych/plugin-preload@1`
  - `https://unpkg.com/@jspsych/plugin-instructions@1`
  - `https://unpkg.com/@jspsych/plugin-canvas-keyboard-response@1`
  - `https://unpkg.com/@jspsych/plugin-survey-multi-choice@1`
- **CDN Connectivity**: If CDNs are blocked, test with `tests/test_cdn.html` to verify access
- **No Local Dependencies**: No package.json, npm install, or build steps required

### Testing and Validation
- **Integration Test**: `tests/test_integration.html` - Complete experiment workflow (5-10 minutes)
- **Memory Task Test**: `tests/test_memory.html` - 4x4 grid memory component validation
- **Collision Detection**: `tests/test_collision_validation.html` - Click target validation
- **Viewing Modes**: 
  - `tests/test_fullscreen.html` - Fullscreen functionality
  - `tests/test_window_drag.html` - Window dragging mode
  - `tests/test_scroll_drag.html` - Scroll interaction mode
- **NEVER CANCEL**: Full experiment takes 15-20 minutes. Set timeout to 30+ minutes for complete validation
- **CRITICAL**: Always test in fullscreen mode - experiment requires fullscreen API access

## Validation Scenarios

### Manual Testing Requirements
**ALWAYS** run through these complete scenarios after making changes:

1. **Quick Validation** (5 minutes):
   - Open `index.html` in browser
   - Complete demographics (age/gender)
   - Run one practice trial in each viewing condition (fullscreen, window, scroll)
   - Verify visual search objects display correctly
   - Confirm mouse clicking and dragging work

2. **Memory Task Validation** (3 minutes):
   - Open `tests/test_memory.html`
   - Complete 4x4 grid memory sequence
   - Verify colored cells display and selection works
   - Confirm memory recall interface functions

3. **Complete Experiment Validation** (20+ minutes):
   - **NEVER CANCEL**: Full experiment has 120 main trials + practice
   - Run complete first block (60 trials without memory)
   - Run complete second block (60 trials with memory)
   - Verify data collection outputs JSON at completion
   - Test all three viewing conditions work correctly

### Critical Functional Areas
- **Mouse Tracking**: Verify `mousePath` data collection includes x, y, time
- **Collision Detection**: Target tolerance of 0.8x object size - test with `test_collision_validation.html`
- **Memory Grid**: 4x4 grid with 2 positions to remember - validate with `test_memory.html`
- **Fullscreen**: Essential for experiment - test fullscreen API access
- **Data Export**: JSON output includes trial data, demographics, mouse trajectories

## Common Tasks

### Testing Changes
- Start web server: `python3 -m http.server 8000`
- Quick test: Open `http://localhost:8000/tests/test_integration.html`
- Full validation: Open `http://localhost:8000` and complete entire experiment
- **Timeout Settings**: Use 30+ minute timeouts for complete experiment runs

### Debugging Common Issues
- **CDN Loading**: Check browser console for 404 errors from unpkg.com
- **Fullscreen Issues**: Modern browsers require user gesture to enter fullscreen
- **Mouse Events**: Verify event listeners attach correctly to canvas elements
- **Memory Task**: Ensure grid cells are clickable and selection state persists
- **Data Collection**: Check jsPsych.data output includes all expected fields

### File Structure Reference
```
wm-itemstructure-effect/
├── index.html                          # Main experiment (1527 lines)
├── styles.css                          # Experiment styling
├── README.md                           # Project documentation (Japanese)
├── COGNITION_RUN_DEPLOYMENT.md         # Deployment guide
├── JSPSYCH_UPGRADE_NOTES.md           # Version upgrade history
└── tests/                              # Test suite (19 files)
    ├── test_integration.html           # Primary integration test
    ├── test_memory.html                # Memory task validation
    ├── test_fullscreen.html            # Fullscreen functionality
    ├── test_collision_validation.html  # Click detection accuracy
    ├── test_window_drag.html           # Window drag interaction
    ├── test_scroll_drag.html           # Scroll interaction
    └── ... (12 additional specialized tests)
```

### Experiment Parameters (from index.html lines 163-178)
```javascript
const params = {
  numObjects: 30,              // Objects per trial
  objectMinSize: 20,           // Minimum object size (px)
  objectMaxSize: 40,           // Maximum object size (px) 
  targetTolerance: 0.8,        // Click tolerance multiplier
  trialsPerCondition: 10,      // Trials per condition
  memoryGridSize: 4,           // Memory grid size (4x4)
  memoryPositions: 2           // Positions to remember
};
```

## Critical Timing Information

### Experiment Duration
- **Practice Phase**: 3-5 minutes (user controls progression)
- **Block 1 (Without Memory)**: 60 trials × ~8 seconds = 8-10 minutes
- **Block 2 (With Memory)**: 60 trials × ~15 seconds = 15-20 minutes
- **Total Experiment Time**: 25-35 minutes for complete run
- **NEVER CANCEL**: Always wait for natural completion or user abort

### Individual Trial Timing
- **Fixation Point**: 1000ms (fixed)
- **Target Display**: 1000ms (fixed) 
- **Visual Search**: Unlimited (user response)
- **Memory Grid**: 3000ms display + unlimited recall
- **Feedback**: 1000ms (fixed)

### Testing Timeouts
- **Quick Test**: 5-10 minutes (single trial per condition)
- **Memory Test**: 3-5 minutes (isolated memory task)
- **Integration Test**: 10-15 minutes (simplified experiment)
- **Full Experiment**: 30-40 minutes (complete validation)
- **CRITICAL**: Set browser timeouts to 45+ minutes for complete runs

## Platform-Specific Notes

### Browser Requirements
- **Fullscreen API**: Required for proper experiment display
- **Canvas Support**: HTML5 canvas for visual search rendering
- **Mouse Events**: Precise mouse tracking and click detection
- **JavaScript ES6+**: Modern JavaScript features used throughout

### Cognition.run Deployment
- Extract JavaScript from `<script>` tags in index.html
- Upload styles.css as separate CSS file
- Configure fullscreen mode in platform settings
- Test all CDN resources load correctly in platform environment

### Known Limitations
- **CDN Dependency**: Requires internet access for jsPsych libraries
- **Fullscreen Requirement**: Experiment designed for fullscreen operation
- **Mouse-Only Input**: No keyboard alternatives for main experiment
- **Browser Compatibility**: Modern browsers only (Chrome, Firefox, Safari, Edge)

## Troubleshooting Guide

### CDN Access Issues
- Symptom: "initJsPsych is not defined" error
- Solution: Test with `tests/test_cdn.html` to verify CDN connectivity
- Workaround: Check browser console for specific CDN blocking errors

### Fullscreen Problems
- Symptom: Experiment displays in window instead of fullscreen
- Solution: Ensure browser allows fullscreen API access
- Test: Use `tests/test_fullscreen.html` to validate fullscreen functionality

### Mouse Interaction Failures
- Symptom: Cannot click objects or drag window/scroll area
- Solution: Verify canvas element creation and event listener attachment
- Test: Use `tests/test_collision_validation.html` for click detection

### Memory Task Issues
- Symptom: Grid cells not clickable or selection not working
- Solution: Check CSS styling and JavaScript event handlers
- Test: Use `tests/test_memory.html` for isolated memory task validation

### Data Collection Problems
- Symptom: No JSON output at experiment end
- Solution: Complete experiment naturally, check browser console for errors
- Validation: Ensure jsPsych.data.displayData() executes successfully

## Quick Command Validation

Before starting work, verify these commands work correctly:

```bash
# 1. Start web server (should start without errors)
python3 -m http.server 8000

# 2. Test main experiment access (should return 200)
curl -s -o /dev/null -w "%{http_code}" http://localhost:8000/

# 3. Test test directory access (should return 200)  
curl -s -o /dev/null -w "%{http_code}" http://localhost:8000/tests/

# 4. Verify file structure
echo "index.html lines: $(wc -l < index.html)"  # Should show: 1527
echo "Test files: $(ls tests/*.html | wc -l)"   # Should show: 19
```

All commands should execute successfully before proceeding with experiment modifications.