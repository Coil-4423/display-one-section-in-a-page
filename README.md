# display-one-section-in-a-page


To display only one `#section` at a time within the same page, you can use JavaScript to dynamically hide and show the relevant sections based on which link is clicked. Here's how you can achieve this:

### HTML Structure

Let's assume you have multiple sections on your page like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Single Section Display</title>
    <style>
        .section {
            display: none; /* Hide all sections by default */
        }

        .section.active {
            display: block; /* Show only the active section */
        }
    </style>
</head>
<body>
    <nav>
        <a href="#section1" onclick="showSection('section1')">Section 1</a>
        <a href="#section2" onclick="showSection('section2')">Section 2</a>
        <a href="#section3" onclick="showSection('section3')">Section 3</a>
    </nav>

    <div id="section1" class="section">
        <h2>Section 1</h2>
        <p>Content for section 1.</p>
    </div>

    <div id="section2" class="section">
        <h2>Section 2</h2>
        <p>Content for section 2.</p>
    </div>

    <div id="section3" class="section">
        <h2>Section 3</h2>
        <p>Content for section 3.</p>
    </div>

    <script>
        function showSection(sectionId) {
            // Hide all sections
            const sections = document.querySelectorAll('.section');
            sections.forEach(section => {
                section.classList.remove('active');
            });

            // Show the selected section
            const activeSection = document.getElementById(sectionId);
            activeSection.classList.add('active');
        }

        // Automatically show the section based on the URL hash when the page loads
        window.onload = function() {
            const hash = window.location.hash.substring(1);
            if (hash) {
                showSection(hash);
            }
        };
    </script>
</body>
</html>
```

### Explanation:

1. **CSS for Displaying Sections:**
   - `.section`: All sections are hidden by default using `display: none;`.
   - `.section.active`: Only the active section (the one currently being viewed) is displayed using `display: block;`.

2. **JavaScript Function `showSection(sectionId)`**:
   - **Hide All Sections**: This function first hides all sections by removing the `active` class from all elements with the class `.section`.
   - **Show the Selected Section**: It then adds the `active` class to the section that matches the `sectionId` passed to the function, making only that section visible.

3. **Handling Link Clicks**:
   - Each link in the navigation calls the `showSection(sectionId)` function with the corresponding section ID (`section1`, `section2`, etc.).
   - The `onclick` event prevents the default anchor link behavior (scrolling to the section) and instead uses JavaScript to control visibility.

4. **Handling Page Load with Hash**:
   - When the page loads, the `window.onload` function checks the current URL's hash (e.g., `#section2`) and automatically displays the corresponding section.
   - This ensures that if a user navigates directly to `example.html#section2`, the correct section will be shown immediately.

### How It Works:
- When a user clicks on a link, only the corresponding section is shown, and all other sections are hidden.
- The page does not scroll since the focus is entirely on displaying one section at a time.
- This method allows for clean navigation within a single page, making it feel like a multi-page experience while keeping everything within one HTML document.