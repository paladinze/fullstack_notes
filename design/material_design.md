# material design

## environemnt
- surface: emulate materials in the physical world
    - all UI elements are based on surfaces
    - always 1 dp thick
    - width & height varies
    - higher elevation cast shadows
    - infinite resolution   
    - content doesn't add thickness
    - limited within bounds of material
    - content and surface could have different behaviours (but also could be the same)
    - input events doesn't pass through
    - multiple surface cannot overlap (one must be elevated)
    - enters the scene by changing opacity, size, position
    - can change shape
    - doesn't bend/fold 
    - can join together

- elevation
    - can be implemented as shadow, opacity or fill style
    - components of the same type should have the same resting elevation


## Color

### Primary Color
- the main color for ui elements

### Secondary Color
- optional
- used for:
    - Floating action buttons
    - Selection controls (sliders & switches)
    - Highlighting selected text
    - Progress bars
    - Links and headlines


### Other colors
- surface colors: color of card, sheets and menus
- background color: appear behind scrollable content
- 'on' colors: color on top of primary colors and secondary colors



