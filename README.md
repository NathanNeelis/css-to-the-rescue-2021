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

## Voortgang
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
* Dark theme
* Waiter asking if you would like the menu back
* Change animation of dropping the paper. Needs checkbox!
* Menu's need to be more interesting. Maybe pin and change animation abit?
* See if we can get scroll-snap to work?
* Link atributes to menu headings to you can tab through?
* Focus within to change the menu item?
* update readme