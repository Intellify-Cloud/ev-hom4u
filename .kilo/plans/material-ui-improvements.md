# Material UI Improvements Plan

## Current State Analysis
- Jekyll static site using Bootstrap 4.5.2 and Font Awesome 5.15.0
- Existing SCSS architecture with variables, mixins, component, and layout partials
- Source styles in `_assets/`, compiled to `assets/bundle.css`
- Uses Poppins font throughout (consistent but not Material-standard)

## Material Design Principles to Apply (without framework change)

### Color System
Current primary: `#00ACC8` (Teal)
Material Design elevation-based colors:
- Surface: `#FFFFFF` (cards, sheets)
- Primary: `#00ACC8` → keep as-is (good Material teal)
- Add Material tints: 50, 100, 200, 300 for hover/disabled states

### Elevation & Shadows (Material standard)
```scss
$elevation-0: none;
$elevation-1: 0 2px 1px -1px rgba(0,0,0,0.2), 0 1px 1px 0 rgba(0,0,0,0.14), 0 1px 3px 0 rgba(0,0,0,0.12);
$elevation-2: 0 3px 1px -2px rgba(0,0,0,0.2), 0 2px 2px 0 rgba(0,0,0,0.14), 0 1px 5px 0 rgba(0,0,0,0.12);
$elevation-3: 0 3px 3px -2px rgba(0,0,0,0.2), 0 3px 4px 0 rgba(0,0,0,0.14), 0 1px 8px 0 rgba(0,0,0,0.12);
$elevation-4: 0 2px 4px -1px rgba(0,0,0,0.2), 0 4px 5px 0 rgba(0,0,0,0.14), 0 1px 10px 0 rgba(0,0,0,0.12);
```

### Border Radius
Material Design uses 4px as standard component radius (not fully rounded)

### Motion
Standard easing: `cubic-bezier(0.4, 0, 0.2, 1)` (standard) or `cubic-bezier(0.2, 0, 0, 1)` (decelerated)

## Specific Modern Material UI Improvements

### Phase 1: Design Token Layer
**Update `_assets/base/_variables.scss`:**
- Add Material elevation shadow variables
- Add Material tints/shades of primary color
- Add focus-ring variables (Material standard: 3px primary glow)
- Add transition timing variables

**Update `_assets/base/_mixins.scss`:**
- Add elevation mixin: `@include elevation(2);`
- Add focus-ring mixin for consistent focus states

### Phase 2: Navigation (Material App Bar)
**Update `_includes/nav.html`:**
- Remove inline `style="background-color:#fff"` - move to CSS
- Add `aria-expanded` handling for toggler

**Update `_assets/components/_navbar.scss`:**
- Use Material elevation on scroll (elevation-2 when shrunk, elevation-1 when top)
- Larger touch targets (minimum 48px height for mobile items)
- Add focus-ring for keyboard navigation
- Material-style underline on hover/active
- Proper color contrast for text (use `$gray-900` instead of `#000`)

### Phase 3: Calculator Cards (Material Cards)
**Update `_includes/calculators.html` & `_includes/calculators2.html`:**
- Add `role="button"` and `tabindex="0"` for keyboard accessibility
- Use `aria-label` on icon-only elements

**Update `_assets/layout/_calculators.scss`:**
- Use Material elevation: elevation-1 default, elevation-2 on hover
- Standard 4px border radius
- Add focus-ring for keyboard users
- Add ripple effect pseudo-element on click
- Use Material-style icon sizing (24px standard)

### Phase 4: Buttons (Material Buttons)
**Update `_assets/components/_buttons.scss`:**
- Material-style raised buttons: elevation-1 default, elevation-2 on hover
- Proper disabled states (20% opacity + no-elevation)
- Focus ring: `box-shadow: 0 0 0 3px rgba($primary, 0.4)`
- Remove scale transform on active - use elevation change instead
- Add ripple effect mixin
- Material-style uppercase text with letter-spacing

### Phase 5: Team Section (Material Avatars)
**Update `_includes/team.html`:**
- Add `alt` attributes to all images (currently missing)
- Add ARIA labels to social links

**Update `_assets/layout/_team.scss`:**
- Material avatar style: circular images with elevation-1
- Add hover elevation
- Better spacing (Material baseline grid: 8px increments)

### Phase 6: Contact Form (Material Text Fields)
**Update `_includes/contact.html` (if form included)**
- Add proper labels for inputs
- Add `aria-describedby` for helper text

**Update `_assets/layout/_contact.scss`:**
- Material text field styling
- Floating labels (optional enhancement)
- Focus states with primary color underline + glow
- Proper input sizing (minimum 48px touch target)

### Phase 7: Accessibility & Reduced Motion
Add to `_assets/base/_page.scss` or new `_assets/base/_a11y.scss`:
```scss
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px rgba($primary, 0.4);
}
```

### Phase 8: Build Verification
- Run `npm run bundle` to compile SCSS
- Verify no regression in Bootstrap functionality
- Test focus states on all interactive elements

## Expected Visual Changes

| Element | Before | After |
|---------|--------|-------|
| Nav bar | Flat, basic background | Elevation on scroll, proper shadow |
| Cards | Basic shadow | Material elevation (1→2 on hover) |
| Buttons | Scale transform on click | Elevation change, ripple effect |
| Focus | Browser default | Consistent Material-style ring |
| Team images | Square with border | Proper avatar styling |

## Implementation Order
1. Design tokens + mixins
2. Buttons (highest reuse)
3. Cards/calculators
4. Navigation
5. Team section
6. Contact form
7. Accessibility polish
