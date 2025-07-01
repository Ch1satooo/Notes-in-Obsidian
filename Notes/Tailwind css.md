## Utility-First Fundamentals
With Tailwind, style elements by applying pre-existing classes directly **in HTML**..
## Handling Hover, Focus, and Other States
### pseudo-class
- Work for ***button, link, list, table, input***.
	hover, active, focus, visited, first, odd/even, enable, required, etc.
	**link**: https://tailwindcss.com/docs/hover-focus-and-other-states#pseudo-class-reference
- Styling based on parent state (***group***)
	Styling based on sibling state (***peer***)
	Styling direct children (***\****)
	Styling based on descendants (***has***)
	**link**: https://tailwindcss.com/docs/hover-focus-and-other-states#styling-based-on-parent-state
### pseudo-element
We can add specific utilities to these elements.
- Before and after
- Placeholder text
- File input buttons
- List markers
- Highlighted text
- First-line and first-letter
- Dialog backdrops
**link**: https://tailwindcss.com/docs/hover-focus-and-other-states#pseudo-elements
## Responsive Design
### Working mobile-first
Use unprefixed utilities to target mobile, and override them at larger breakpoints: 
```javascript
<!-- This center text on mobile, and left align it on screens 640px and wider -->
<div class="text-center sm:text-left"></div>
```

By default, styles applied by rules like `md:flex` will apply at that breakpoint and stay applied at **larger breakpoints**.
## Dark Mode
Tailwind includes a `dark` variant that lets you style your site differently when dark mode is enabled:
```javascript
<p class="text-slate-500 dark:text-slate-400 mt-2 text-sm"> 
	Dark mode will change text color here.
</p>
```
