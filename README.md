# Yet Another Related Posts Plugin Modern Grid layout

# YARPP Custom Grid CSS

## Overview

This repository provides custom CSS to style the output of the "Yet Another Related Posts Plugin" (YARPP) for WordPress. It replaces the default YARPP styling to display related posts in a modern, responsive grid layout.

The default behaviour implemented here is:

*   **Desktop:** A 4-column grid.
*   **Mobile (<= 768px):** A 2-column grid.
*   Uses CSS Grid for layout.
*   Thumbnails fill their allotted space using `object-fit: cover` with a default 3:2 aspect ratio.

## Features

*   Responsive grid layout using CSS Grid.
*   Configurable number of columns for desktop and mobile.
*   Images fill their container while maintaining aspect ratio (crops if necessary).
*   Consistent visual appearance for related post thumbnails.
*   Requires disabling default YARPP styles for a clean slate.

## Prerequisites: Disable Default YARPP Styles

**This step is essential!** Before applying this custom CSS, you MUST disable the default stylesheets loaded by YARPP. Otherwise, conflicting styles will likely cause layout issues.

1.  Open your **active WordPress theme's `functions.php` file**.
    *   **Important:** If you are using a child theme (recommended), add this code to the child theme's `functions.php`. If you add it to a parent theme's `functions.php`, your changes will be lost when the parent theme updates.
2.  Add the following PHP code snippet to the end of the file (before any closing `?>` tag if one exists):

    ```php
    /**
     * Disable Default YARPP Stylesheets.
     * This is necessary to use completely custom styling.
     */
    add_filter( 'yarpp_enqueue_related_style', '__return_false' ); // Disables base related content CSS
    add_filter( 'yarpp_enqueue_thumbnails_style', '__return_false' ); // Disables thumbnail-specific CSS
    ```

3.  Save the `functions.php` file.

## Installation / Usage

1.  **Complete the Prerequisite step above** to disable the default YARPP styles.
2.  Copy the CSS code from the `yarpp-custom-grid.css` file (or copy the CSS provided in the previous steps).
3.  Add this CSS code to your WordPress site. You have several options:
    *   **Theme Customizer:** Go to `Appearance` -> `Customize` -> `Additional CSS` and paste the code there.
    *   **Child Theme Stylesheet:** Add the code to your child theme's `style.css` file.
    *   **Custom CSS Plugin:** Use a dedicated plugin for adding custom CSS (like Simple Custom CSS and JS, WPCodeBox, etc.) and create a new CSS entry.
    *   **(Advanced) Enqueueing:** Properly enqueue this CSS file via your theme's `functions.php` using `wp_enqueue_style`.
4.  Clear any caching plugins you might be using (WordPress cache, browser cache, CDN cache) to ensure the new styles are loaded.
5.  Visit a page or post where YARPP related posts are displayed to see the new grid layout.

## CSS Explanation

*   **`.yarpp-thumbnails-horizontal`**: This `div` (which contains the `<a>` tags for each related post) is targeted as the `display: grid` container.
*   **`grid-template-columns: repeat(4, minmax(0, 1fr));`**: Creates the 4 equal-width, flexible columns for desktop. `minmax(0, 1fr)` helps prevent overflow issues.
*   **`gap: 1.5em;`**: Defines the spacing between grid items.
*   **`@media (max-width: 768px)`**: A media query changes the `grid-template-columns` to `repeat(2, minmax(0, 1fr))` for screens 768px wide or narrower, creating the 2-column layout.
*   **`.yarpp-thumbnail img`**: Styles the thumbnail image.
    *   `width: 100%;` / `aspect-ratio: 3 / 2;`: Makes the image *container* fill the width and maintain a 3:2 aspect ratio.
    *   `object-fit: cover;`: Makes the image *content* scale to cover this container, cropping if necessary.

## Customization

You can easily adjust the CSS to fit your needs:

*   **Number of Columns:** Change the `repeat(4, ...)` value for desktop and `repeat(2, ...)` within the media query for mobile.
*   **Breakpoint:** Modify the `max-width: 768px` value in the `@media` query to change when the layout switches to 2 columns.
*   **Spacing:** Adjust the `gap` value (e.g., `1em`, `20px`).
*   **Image Aspect Ratio:** Change `aspect-ratio: 3 / 2;` to another ratio like `16 / 9`, `1 / 1` (square), etc.

## Important Notes

*   This CSS assumes the standard HTML structure output by the YARPP Thumbnails template. If YARPP updates and changes its HTML structure or class names significantly, this custom CSS might need adjustments.
*   Always test changes on a staging site before applying them to your live website.

## License

(Optional: Add a license if you plan to share this publicly, e.g., MIT License)
