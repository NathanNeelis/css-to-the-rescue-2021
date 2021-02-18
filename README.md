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
  <summary>Variable fonts in CSS</summary>

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
  <summary>Accessibility in CSS</summary>

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
  <summary>Falling paper animation in CSS</summary>

```HTML

```

 ```CSS

 ```
</details>

#### Some other interaction
At the end of the week, I added some simple interaction to the menu's. This is what it looks like. But have in mind, this still needs an update to make it more exciting.
![CSS_Hover-effects](https://user-images.githubusercontent.com/55492381/108344362-57d1a400-71dd-11eb-8ee9-76c67e35556c.gif)  

<details>
  <summary>Some other interactions</summary>

```HTML

```

 ```CSS

 ```
</details>





## afronding