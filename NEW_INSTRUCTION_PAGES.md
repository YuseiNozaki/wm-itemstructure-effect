# New Instruction Pages - Testing Guide

This document describes the new instruction page implementation for the WM item structure effect experiment.

## Implementation Overview

Four new instruction pages have been created to replace the old complex pages:

### 1. Initial Explanation for Memory-First Group (前半が記憶課題グループ)
- **When shown**: For participants where `memoryFirstCondition = true`
- **Content**: 5-step explanation including memory panel task
- **Location**: After demographics, before practice
- **Button**: "練習に進む" (triggers fullscreen mode)

### 2. Initial Explanation for Memory-Second Group (後半が記憶課題グループ)  
- **When shown**: For participants where `memoryFirstCondition = false`
- **Content**: 3-step explanation for visual search only
- **Location**: After demographics, before practice
- **Button**: "練習に進む" (triggers fullscreen mode)

### 3. Midpoint Explanation for Memory-First Group (前半が記憶課題グループ)
- **When shown**: For participants where `memoryFirstCondition = true`
- **Content**: Notification that memory task is removed in second half
- **Location**: Between first and second block
- **Button**: "後半開始"

### 4. Midpoint Explanation for Memory-Second Group (後半が記憶課題グループ)
- **When shown**: For participants where `memoryFirstCondition = false`  
- **Content**: Explanation of new memory task being added
- **Location**: Between first and second block
- **Button**: "後半開始"

## Design Principles

- **No emojis**: Completely serious, professional design
- **Simple layout**: Clean numbered steps with clear visual hierarchy
- **Consistent styling**: Blue (#007bff) primary color theme
- **Clear typography**: Proper spacing and readability
- **Minimal content**: Essential information only

## Technical Implementation

### Conditional Display Logic
```javascript
// Initial explanations
const conditionalInitialExplanation = {
  timeline: [initialExplanationMemoryFirst],
  conditional_function: function() {
    return memoryFirstCondition;
  }
};

const conditionalInitialExplanationSecond = {
  timeline: [initialExplanationMemorySecond], 
  conditional_function: function() {
    return !memoryFirstCondition;
  }
};

// Similar structure for midpoint explanations
```

### Timeline Changes
```javascript
const timeline = [
  welcome,
  informedConsent,
  demographics,
  conditionalInitialExplanation,      // NEW: Shows based on counterbalancing
  conditionalInitialExplanationSecond, // NEW: Shows based on counterbalancing  
  practiceProcedure,                   // Fullscreen activation moved here
  mainExperimentStart,
  firstBlockProcedure,
  conditionalMidpointExplanation,      // NEW: Shows based on counterbalancing
  conditionalMidpointExplanationSecond, // NEW: Shows based on counterbalancing
  secondBlockProcedure,
  endScreen
];
```

## Testing Instructions

### Manual Testing (requires CDN access)

1. **Test Memory-First Group**:
   - Set CONDITION to odd number (or ensure memoryFirstCondition = true)
   - Verify initial explanation shows 5 steps including memory task
   - Verify midpoint explanation mentions memory task removal

2. **Test Memory-Second Group**:
   - Set CONDITION to even number (or ensure memoryFirstCondition = false)
   - Verify initial explanation shows 3 steps (visual search only)
   - Verify midpoint explanation explains memory task addition

3. **Fullscreen Timing**:
   - Verify fullscreen does NOT activate during initial explanation
   - Verify fullscreen activates when clicking "練習に進む" button

### Key Validation Points

- [ ] Counterbalancing correctly determines which pages are shown
- [ ] Only appropriate pages display for each group
- [ ] Fullscreen activation occurs at practice start, not instruction start
- [ ] All button interactions work correctly
- [ ] Content is clear and professional (no emojis)
- [ ] Typography and styling is consistent

## Files Modified

- **index.html**: Main experiment file with new instruction pages
- **test_new_instructions.html**: Standalone testing tool for instruction pages

## Removed Legacy Code

- `experimentInstructions`: Complex page with emojis and lengthy content  
- `practiceExplanation`: Simple practice intro page
- `midpointMessage`: Basic halfway message
- `wmTaskExplanation`: Detailed memory task explanation with visual examples

All legacy code has been completely removed and replaced with the new conditional system.