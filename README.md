## Creating a Responsive Image Gallery using HTML and CSS: A Step-by-Step Tutorial

In this tutorial, I will guide you through creating a responsive image gallery using HTML and CSS. This gallery will feature sixteen image placeholders, each with a transparent overlay and an effect when you hover over them. By the end of this tutorial, you will have a beautiful and responsive image gallery that you can customize for your project. This gallery is part of my final project for the Web Development Introduction course, where I've learned HTML and CSS. My next goal is to enhance this gallery's functionality by incorporating JavaScript and a database to further expand its capabilities.



 1. ### Set Up Your Project
     1.  Create a root folder for your project called "**my-image-gallery**".
     2.  Inside this root folder, create a subfolder named "**assets**".
     3.  Inside the "assets" folder, create  two subfolders named "**img** and **style**".
     4.  Create an "index.html" file and place it in the "my-image-gallery" root folder.
     5.  Create a "style.css" file and store it in the "style" folder.
     6. Create a global.css file and store it in the "style" folder.
     7.  Save all your images in the "img" folder.

This basic hierarchical structure will help keep your project organized and make it easier to manage your files.
    
 2. ### Build the HTML Structure 

	The HTML structure is the foundation of your image gallery. 
	Open the **index.html** file and start building the basic structure:
  ```sh
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Responsive Image Gallery</title>
    <link rel="stylesheet" href="./assets/style/style.css" media="all">
</head>
<body>
    <div class="container">
        <div class="row">
            <div class="column one">
                <a class="transparent-button" href="#"></a>
            </div>
            <!-- Repeat the above structure for the remaining columns (two to sixteen) -->
        </div>
    </div>
</body>
</html>
   ```
  -   `<div class="container">`: A `<div>` element with the class "container" that acts as a container for the entire page.
    
-   `<div class="row">`: Another `<div>` element with the class "row" used to create a row for organizing the image columns within the container.
    
-   `<div class="column one">`: A `<div>` element with the class "column one," representing the first image column in the gallery. 
    
-   `<a class="transparent-button" href="#"> </a>`: An anchor element (`<a>`) styled as a transparent button. It creates an interactive overlay for the image column. The `href="#"` attribute specifies that the link doesn't lead to another page or location.

3. ### Create a "global.css" file

This file houses the CSS styles that are shared throughout your entire website, including styles for headers and paragraphs. In this file, you can define properties such as font-size, font-family, colors and more. 
1.  Create a file named "global.css" in your project's root directory.
2.  Add the following CSS code to "global.css" to define the styles. Adjust to your preferences.

  ```sh
 /* Reset some default styles */  
 body, h1, h2, h3, p { 
 margin: 0; padding: 0; 
 }

body { 
	font-family: Arial, sans-serif; font-size: 16px; 
}

/* Define styles for headers */
h1 {
font-size: 24px;
color: var(--app-white);
letter-spacing: 0.4px;
line-height: 2;
}
/* Define styles for paragraphs */
p {
font-size:16px;
color: var(--app-dark-gray);
line-height: 1.4;
margin-bottom: 30px;
}

/* It is used to store a specific color value.
In your code, you can use `var(--app-light-gray-bg)
to reference this color value wherever you need it */

:root {
	--app-light-gray: #ababab;
	--app-dark-gray: #141414;
	--app-gray-background: #e9edf2;
	--app-white: #fff;
}
  ```
  
  3. Link the "global.css" file to your "index.html" by adding the following line inside the `<head>` section:
```sh
<link rel="stylesheet" href="./assets/style/global.css">
```

4. ### Write the CSS Stylesheets 
A CSS (Cascading Style Sheets) file is a document containing code that defines the visual styling and layout of HTML elements on a webpage.

 Open the `gallery.css` file and write the initial styling for your gallery. 
   ```sh
@charset  "utf=8";

.container {
width: min(100%  -  30px, 1080px);
margin-inline: auto;
}

.row {
display: flex;
flex-wrap: wrap;
gap: 20px;
}

.column {
flex: 0  1  auto;
width: calc(25%  -  15px);
padding-bottom: calc(25%  -  15px);
border-radius: 5px;
box-shadow: 1px  1px  2px  rgba(0, 0, 0, 0.1);
overflow: hidden;
position: relative;
}

.one {
background-color: var(--app-gray-background);
background-image: linear-gradient(to  bottom, transparent  75%, rgba(0, 0, 0, 0.5) 95%), url('../img/featured-img1.jpg');
background-size: cover;
position: relative;
}
/* Replicate the style used for `.one` across the other div elements
(`.two`, `.three`, `.four`, etc.), changing only the featured image
URL for each div. */

.one::after {
content: url('../img/user-icon.png') " John Smith";
position: absolute;
bottom: 10px;
left: 10px;
color: var(--app-white); 
font-weight: 400;
text-shadow: 2px  2px  4px  rgba(0, 0, 0, 0.9);
}
/* Replicate the style used for `.one::after` across the other div elements
(`.two::after`, `.three::after`, `.four::after`, etc.), changing only the 
content: "name" for each div.  */
 ```
 
- `@charset 'utf=8';` is a CSS rule that specifies the character encoding of the style sheet as UTF-8, ensuring proper text rendering, especially for non-ASCII characters.

- The `.container` class sets the width to a minimum of 100% minus 30px and a maximum of 1080px while centring it horizontally.

- The `.row` class utilizes flexbox to create a flexible layout with wrapping elements and a 20px gap between them.

-    The `.column` class is used to define the styling for individual columns within the layout.
	 -   This class has a flexbox with a flex-grow value of 0, a flex-shrink value of 1, and an automatic flex-basis.
	 -    Each column is set to occupy 25% of its container's width minus 15px for a gap.
	 -   It includes a 5px border radius, a subtle box-shadow for a lifted effect, and hidden overflow.
	 -   The columns are relatively positioned, allowing for precise placement within the container.
	
- The `.one` class sets the background color, creates a gradient overlay, and positions a background image (the image of your gallery).

- The `.one::after` class creates overlay content, including a user icon and text with styles, at an absolute position below and to the left of the ".one" element.

5. ## Create the overlay effect

Create a style that forms a button overlaying an image upon mouse hover with a transparent overlay. The overlay should darken the image and reveal a magnifying glass icon. It enhances the intuitiveness of zooming in on the image.

  ```sh
.transparent-button {
position: absolute;
width: 100%;
height: 100%;
background-color: transparent;
border: none;
cursor: pointer;
outline: none;
}

.transparent-button:hover {
background-color: var(--app-dark-overlay);
mix-blend-mode:normal;
transition: background-color 0.3s  ease-in-out;
color: var(--app-white);
font-weight: 400;
}

.transparent-button:hover::before {
content: url(../img/zoom-64.png);
font-size: 100px;
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
margin-right: 8px;
transition: opacity 1s  ease-in-out;
}
   ```

 - `.transparent-button`:
   
   -   Defines base styles for a transparent button.
   -   Occupies full width and height of its parent element.
   -   Changes the mouse cursor to a pointer when hovered.
   
  -  `.transparent-button:hover`:
   
	   -   Defines styles when the button is being hovered over.
	   -   Applies a dark overlay to the background and changes the text color to white.
	   -   Creates a smooth transition effect when altering the background color.
	   
-  `.transparent-button:hover::before`:
   
   -   Defines styles for a pseudo-element placed before the button on hover.
   -   Inserts a magnifying glass image before the button.
   -   Centers the magnifying glass image and applies a smooth opacity transition.

    
6. ## Implement Responsiveness 

Responsive web design is essential to ensure that a website adapts to various screen sizes and devices, offering a consistent and user-friendly experience. The code below should be placed in your stylesheet and utilizes media queries to customize the gallery's appearance for different devices and browser sizes.

  ```sh
@media  screen  and (max-width: 960px) {
	.column {
	width: calc(50%  -  10px);
	padding-bottom: calc(50%  -  10px)
	}
}

@media  screen  and (max-width: 768px) {
	.column {
	width: 100%;
	padding-bottom: 100%;
	}
}

@media  screen  and (max-width: 480px) {
	.one, .two, .three, .four, .five, .six, .seven, .eight, .nine, .ten, .eleven, .twelve, .thirteen, .fourteen, .fifteen, .sixteen {
	width: 100%;
	padding-bottom: 100%;
	}
}
   ```
-   `@media screen and (max-width: 960px)`: For screens with a width of 960 pixels or less. It adjusts its width to occupy 50% of the container's width minus 10px for spacing, creating a 2-column layout, and sets the padding-bottom to the same value, maintaining a square aspect ratio for each column.

-   `@media screen and (max-width: 768px)`: For screens with a width of 768 pixels or less. It sets their width to 100%, causing them to stack vertically and take up the full width of the container, effectively creating a single-column layout for smaller screens.

-   `@media screen and (max-width: 480px)`: For screens 480 pixels or less. It sets both the width and padding-bottom of these elements to 100%, making them stack vertically and occupy the full width of the container. This is typically used to adapt the layout for very small screens, like mobile devices.

7. ## Project Result

Now you have a beautiful and responsive image gallery that can serve various purposes, whether it's showcasing artwork or displaying products. The images below show how the gallery appears within a webpage I've created on different screen sizes. The search tool is illustrative, and its functionality will be implemented in a future project.

Feel free to add more features to make it unique. This tutorial serves as a foundation for you to further develop your skills and expand your knowledge.

**Happy coding!**

