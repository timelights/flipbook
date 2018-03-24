# Flip Book
A simple demo of flip animation for book pages. [See demo](https://timelights.github.io/flipbook/)\
See also a simple [CSS 3D Flip Card](https://github.com/timelights/flip).

### HTML
```html
<div class="pages viewport"> <!-- the DOM-parent with a perspective -->
	
	<!-- Last Page (outback) -->
	<div class="page outback"> <!-- .page is a 3d-object -->
		<div class="content front <your-css>"></div> <!-- the front face -->
		<div class="content back <your-css>"></div> <!-- the back face -->
	</div>

	<div class="page"> <!-- .page is a 3d-object -->
		<div class="content front <your-css>"></div> <!-- the front face -->
		<div class="content back <your-css>"></div> <!-- the back face -->
	</div>

	<!-- First Page (outfront) -->
	<div class="page outfront"> <!-- .page is a 3d-object -->
		<div class="content front <your-css>"></div> <!-- the front face -->
		<div class="content back <your-css>"></div> <!-- the back face -->
	</div>

</div>
```

What is ```<your-css>```?
```
/* your css */
.custom-content {
	background-image: url(...)
}
```

### CSS
```css
/* of course there must be a size for a 3d object */
.book {
	width: 60%; /* adjust this to tweak [ transform-origin: left ] of the .page DOM */
	height: 90%;
	margin: auto;
	/*border: 1px solid black;*/ /* uncomment to see debug guidelines */
}

.pages {
	float: right;
	width: 50%; /* FIXED 50% of Total Width when double-page is present */
	height: 100%; 
	transform: translateX(-50%);
	transition: transform 0.5s;
}

/* the trigger may not always be this DOM */
/*.page:hover  {
	transform: rotateY(-180deg)
}*/


/* every 3d needs a perspective view */
.viewport {
	perspective: 1000px;
}

/* 
a flat 3d object
	> MUST always have a [ transform-style: preserve-3d ]
	> must be inside a DOM-parent with a perspective!
	> usually has a front and back face
*/
.page {
	cursor: pointer; /* optional */
	width: 100%; 
	height: 100%;
	transform-style: preserve-3d; 
	transition: all .5s ease-out; 
	position: absolute; 
	transform-origin: left; 
	/*border:1px solid lightgreen;*/ /* uncomment to see debug guidelines of transform-origin */
}

/* the front and back face */
.content {
	/* customization */
	background-size: contain;
	background-repeat: no-repeat;
	background-position: center;
	/*box-shadow: inset 0 0 50px rgba(0,0,0,0.3);*/

	/* IMPORTANT */
	width:100%;
	height:100%;
	position: absolute;
	backface-visibility: hidden;
}

/* the front and back face must have characteristics */
.front { transform: rotateY(0deg) }
.back { transform: rotateY(180deg) }

/* content (front/back) customizations */
.your-css { background-image: url(...) }
```