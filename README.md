# Problem: Create an Interactive Shape-Based UI

## Functional Requirements

1. **Create an empty box where array value is 1.**
2. **User Interaction:**
   - The user can select a box.
   - Upon selection, the box background color should change to `#0bcc59`.
3. **Auto-Deselection:**
   - Once all boxes are selected, the boxes should auto-deselect in the order they were selected.
   - Deselection should be non-interruptible—once started, it cannot be stopped.
4. **Disable Interaction During Deselection:**
   - While boxes are auto-deselecting, the user should not be able to select any box. Box interaction should be disabled during this phase.

## Mockups

- **Shape with Empty Boxes**: Placeholder showing initial shape with empty boxes.
- **Shape with Some Boxes Filled**: Placeholder showing partially filled shape based on user interaction.

## Files (Starting Point)
// Use this data to create the shape
const BOX_DATA = [
  [1, 1, 1],
  [1, 0, 0],
  [1, 1, 1],
];
