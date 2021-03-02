<!-- livelink  -->


## The plan
### Assignment
I choose to do the CSS Zen Garden assignment.  
For this assignment we got to choose between a restaurant menu html file or a page in a digital magazine. I choose the restaurant menu, for the sole reason that I long for a night out again.  
  
### The following list are techniques I would like to get a closer look at:  
* Accessibilty 
* Darkmode 
* Perhaps other modes? 
* Calc()
* Custom properties
* Parallax
* grid
* Transform 
* Animate

### Requirements:
* Responsive without media queries
* Completely accessible according to the AAA WCAG terms

## Progress
### Inpsiration
Before starting, I browsed around looking for inspiration.  
In some images I found a menu on a clipboard, en though it be fun to try to create something like a flip board. Because it is in a way pretty old-school to use a clip-board menu but there lots of possibilities to make this lay-out work and fun in a digital environment.

<img width="307" alt="Clipboard-menu as inspiration" src="https://user-images.githubusercontent.com/55492381/108341842-666a8c00-71da-11eb-9481-4df8a9099955.png">  

### Initial idea
So grabbing pen and paper, I started drawing some ideas on paper.  
I came up with a clipboard where you could flip through the menu pages, as you can see on the sketched storyboard below.  
  
Sketched clipboard menu  
<img width="307" alt="Clipboard-menu sketched" src="https://user-images.githubusercontent.com/55492381/108342083-af224500-71da-11eb-96e6-c0a0ce0c0c4c.jpg">  

Interaction storyboard clipboard menu  
![Clipboard storyboard](https://user-images.githubusercontent.com/55492381/108342217-d6791200-71da-11eb-80f5-348e98c8dafc.JPG)


### Experimenten with tecniques
#### Variable fonts
I learned of the existence of variable fonts and started experimenten with it in the logo of the restaurant. As you can see in the image below, the "&" character becomes thinner and fatter smoothly.  
  
![CSS_Variable-fonts](https://user-images.githubusercontent.com/55492381/108343600-6c616c80-71dc-11eb-838e-1d7bd140d965.gif)  

<details>
  <summary>Variable fonts in CSS code</summary>

 ```CSS
@font-face {
    font-family: "IBM Plex Sans Roman";
    src: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/85648/IBMPlexSansVar-Roman.ttf");
}

:root {
    --font-heading: 'IBM Plex Sans Roman', Times;
}

h1,
h2,
h3 {
    font-family: var(--font-heading);
}

h1 span:nth-child(2) {
    ...
    font-variation-settings: 'wght'100, 'wdth'85;
    animation: breathe 4s infinite both;
}

@keyframes breathe {
    0% {
        font-variation-settings: 'wght'100, 'wdth'85;
    }

    60% {
        font-variation-settings: 'wght'700, 'wdth'85;
    }

    100% {
        font-variation-settings: 'wght'100, 'wdth'85;
    }
}
 ```
</details>


#### Accessibility
In the thema session about accesssibility I learned of the 'skip to content' button. But as Vasilis said, it can be that the person, trying to use this technique does not understand the term 'content'. In my menu I gave this button a humoristic spin, you can skip all of the menu and skip right to the desserts!  
  
![CSS_Accessibility](https://user-images.githubusercontent.com/55492381/108343895-c6fac880-71dc-11eb-9f32-2fcabd29dc94.gif)  

<details>
  <summary>Accessibility in CSS code</summary>

```HTML
<a href="#sweets">Go straight to the sweets<span>🎂</span> </a>
```

 ```CSS
/* ACCESSIBILITY  */
body>a:first-child {
    background-color: var(--accessibility);
    text-decoration: underline;
    padding: 1rem 4rem 1rem 1rem;
    color: var(--white);
    outline: none;

}

.hidden,
[href="#sweets"] {
    clip: rect(0 0 0 0);
    position: absolute;
    top: -1em;
    transition: .2s;
}

.hidden,
[href="#sweets"]:focus {
    clip: auto;
    top: 0;
}

[href="#sweets"] span {
    width: 1em;
    height: 1em;
    display: inline-block;
    position: absolute;
    top: 0;
    opacity: 0;
}

[href="#sweets"]:focus span {
    animation-name: grow;
    animation-duration: 2s;
    animation-iteration-count: 1;
    animation-delay: .3s;
    transform-origin: center center;
    animation-fill-mode: forwards;
    padding-left: .5rem;
}

/* END ACCESSIBILITY  */
 ```
</details>

#### Accessibility continued
To be able to walk through the menu card without a mouse I added links to the headings. This way you can tab through the menu cards dishes. The elements change on tabbing because I used the `focus-within` pseudo class. Also I use a certain color now to highlight everything done for accessibility. This way the user easily notices where he is on the page and what is changed by, for example, tabbing.  
  
-- image --  
  
<details>
  <summary>More accessibility in CSS code</summary>

```HTML
<article id="smokedFish">
    <h3><a href="#smokedFish">smoked fish</a></h3>
    <p><em>Serves 3 - 4 people</em> with cream cheese, onion, tomato, capers &amp; new potato salad and Russ &amp; daughters bread basket</p>
    <div>60</div>
</article>
```

 ```CSS
/* ACCESSIBILITY  */

/* STYLING LINKS WITH FOCUS  */
a {
    text-decoration: none;
    color: inherit;
    cursor: auto;
}

a:focus {
    outline: var(--accessibility) dashed;
    padding: 0 1rem;
}

/* STYLING DISHES TAB-ORDER IN MENU CARD  */
article a:focus {
    outline: none;
    padding: 0;
}

article:focus-within {
    /* background: var(--green); */
    background: var(--accessibility);
}

article:focus-within h3,
article:focus-within p {
    color: white;
}
/* END ACCESSIBILITY  */
 ```
</details>


#### Animation - part 1
When hovering over the clip from the clipboard, you loose your menu card. Woops! 
In an animation the paper slides off-screen. This is the first part of the animation that I got working. What I'm still planning on doing is that the menu doenst come back at all, and that you will see a figure, a waiter, that asks if you would like a new menu. After accepting, the menu appears again.  
  
![CSS_Falling-Paper-animation](https://user-images.githubusercontent.com/55492381/108344228-2ce75000-71dd-11eb-8328-dbaf521bbb37.gif)  

<details>
  <summary>Falling paper animation in CSS code</summary>

```HTML
    <div class="clipWrapper">
        <div class="clip"></div>
    </div>

    <main>
        <section>
            ...
        </section>
        ...
    </main>
```

 ```CSS
.clipWrapper:hover~main>section {
    animation-name: falldown;
    animation-duration: 4s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
    animation-delay: 1s;
    animation-timing-function: cubic-bezier(0.250, 0.460, 0.455, 1.310);
}

@keyframes falldown {
    0% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(600vh);
    }

    60% {
        transform: translateY(600vh);
    }

    90% {
        transform: translateY(0);
    }
}
 ```
</details>


#### Animation - part 2
Instead of hovering, I changed the clip to a checkbox.   
Once you click the clip, you loose your menu!   
But what now..? After about 10 seconds a waiter appears to ask if you lost your menu. You can ask him for a new one. If you do this, a new menu will appear.
  
-- image --   
  

<details>
  <summary>Falling paper animation in CSS code</summary>

```HTML
    <!-- Loose the menu  -->
    <div>
        <label for="menuCard" class="clip"></label>
    </div>
    <input type="checkbox" id="menuCard" name="menucard">

    <!-- Retrieve the menu  -->
    <div>
        <p><span>👨🏻‍🍳</span></p>
        <p>Lost your menu?</p>
        <label for="menuCard">Yes, I would like a new one please.</label>
    </div>

```

 ```CSS
/* DROPPING PAPER ANIMATION  */
input[type=checkbox]:checked~main>div {
    transform: translateY(calc(100% + 10em));
    transition: transform .4s cubic-bezier(1, -0.11, .87, .73);
    transition-delay: 1s;

}

input[type=checkbox]:not(:checked)~main>div {
    transform: translateY(calc(0));
    transition: transform .4s cubic-bezier(1, -0.11, .43, 1.21);
    transition-delay: 1.5s;
}

input[type=checkbox] {
    opacity: 0;
}

/* WAITER ASKING MENU CARD  */
/* 👨🏻‍🍳  */
body>div:nth-of-type(2) {
    width: 15em;
    height: 10em;
    position: absolute;
    top: calc(50% + 90vh);
    left: calc(50% - 7.5em);
    margin: 0 auto;
    z-index: 7;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;


    text-align: center;
    opacity: 0;
    transition: opacity 1s ease-out;
    transition-delay: .5s;
}

/* CHECKBOX UNCHECKED, WAITER RUNS TO GET MENU  */
body>div:nth-of-type(2) span {
    display: block;
    font-size: 3em;
    transform: translateX(70vw);
    transition: transform 1.5s cubic-bezier(.12, -0.46, .43, 1.41);
    transition-delay: .5s;
}

body>div:nth-of-type(2) label {
    margin: 1rem;
    padding: 1rem;
    background: var(--green);
    border-radius: .5rem;
    color: var(--white);
    box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.57);
    transition: all .5s ease-in-out;
}

body>div:nth-of-type(2) label:hover {
    background: var(--white);
    color: var(--green);
    box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.57);
    transition: all .5s ease-in-out;
}

input[type=checkbox]:checked~div:nth-of-type(2) {
    opacity: 1;
    transition: opacity .5s ease-in;
    transition-delay: 5s;
    z-index: 10;
}

/* checked  appear waiter*/
input[type=checkbox]:checked~div:nth-of-type(2) span {
    transform: translateX(0);
    transition: transform 1.5s cubic-bezier(.12, -0.46, .43, 1.41);
    transition-delay: 5s;
}

 ```
</details>

#### Some other interaction
At the end of the week, I added some simple interaction to the menu's. This is what it looks like. But have in mind, this still needs an update to make it more exciting.  
  
![CSS_Hover-effects](https://user-images.githubusercontent.com/55492381/108344362-57d1a400-71dd-11eb-8ee9-76c67e35556c.gif)  

<details>
  <summary>Some other interactions in css code</summary>

 ```CSS
h2:hover {
    font-variation-settings: 'wght'600, 'wdth'185;
    transition: font-variation-settings 2s ease-in-out;
}
```
 ```CSS
article:hover {
    animation-name: wiggle;
    animation-duration: .5s;
    animation-iteration-count: 1;
    animation-timing-function: cubic-bezier(0.250, 0.460, 0.455, 1.310);
}
```
 ```CSS
 article div::after {
    background-color: var(--green);
    position: absolute;
    width: 2rem;
    height: 2rem;
    content: "€";
    border-radius: 50%;
    align-items: center;
    justify-content: center;
    display: flex;
    font-family: var(--font-heading);
    animation-name: breathe;
    animation-iteration-count: infinite;
    animation-duration: 4s;
    transition: .5s;
}

article div:hover::after {
    background-color: transparent;
    content: "";
    transition: .5s;
}

section article:nth-child(odd) div::after {
    animation-delay: 1s;
}

section article:nth-child(even) div::after {
    animation-delay: 2s;
}

 ```
</details>

#### Clamp()
Using clamp was totally new for me. And WOW!.. What an amazing technique. In my menu card I most ofent used this technique for the font-size. Setting a minimum optimal and maximum font-size all in one go.

<details>
  <summary>Clamp in css code</summary>

 ```CSS
body> :nth-child(2) p {
    ...
    font-size: clamp(1.6rem, 6vw, 4rem);
    ...
}

h1 {
    font-size: clamp(2rem, 8vw, 6rem);
    ...
}
 ```
</details>

#### Calc
Using Calc was also new for me, just like clamp, I didnt even know it was out there. But now I know, I use it alot! For example to calculate the padding or to position something right in the middle. Now I dont have to calculate this myself anymore, just put it in one line of code.

<details>
  <summary>Using Calc in css code</summary>

 ```CSS

main {
    ...
    overflow-y: scroll;
    padding: 0 calc(5% - 10px) 0 5%;
    /* The minus 10px is for the scroll bar that has a widht of 10px*/
    ...
}

article div {
    ...
    position: absolute;
    bottom: -1rem;
    left: calc(50% - 1.25rem);
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 50%;
    ...
}

 ```
</details>

#### Custom properties
I had seen custom properties before, but I always though they where the result of a precompressor like SCSS. So I never got into it. But since this course, all has been revealed. Custom properties are awesome! Still I have to get used to working with them, and find the extend to what is possible with it. In this assignment, I used basic custom properties to get familiar with them.

<details>
  <summary>Custom properties in css code</summary>

 ```CSS
:root {
    --green: #189100;
    --white: #fff;
    --gray: #ebebeb;
    --black: #333333;

    --font-heading: 'IBM Plex Sans Roman', Times;
    --font-body: 'Catamaran', sans-serif;
}

h1,
h2,
h3 {
    font-family: var(--font-heading);
}

a:first-child {
    background-color: var(--green);
}

 ```
</details>

#### Grid
I have used Grid before, but I always prefered using flexbox. For this assignment I though it neccecarily to get out of my comfort zone and dive in to Grid once again. And once again, it amazes me how well this works in combination with responsiveness without media queries. Why am I not using this more often?? Well, now I will.

<details>
  <summary>Grid in css code</summary>

```HTML
    <main>
        <section>
            <header>
                ...
            </header>
            <article>
                ...
            </article>
            <article>
                ...
            </article>
            ...
        </section>
        ...
    </main>
```

 ```CSS
section {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(12em, 1fr));
    justify-self: center;
    column-gap: 1em;
    row-gap: 2em;
}

section header {
    margin-bottom: 1rem;
    grid-column: 1 / -1;
}

 ```
</details>


## To do
* Dark theme -- FIXED
* Waiter asking if you would like the menu back -- FIXED
* Change animation of dropping the paper. Needs checkbox! -- FIXED
* Menu's need to be more interesting. Maybe pin and change animation abit? -- DONE
* Blockquotes styling -- DONE
* Link atributes to menu headings to you can tab through? -- DONE
* Focus within to change the menu item? -- DONE
* update readme