div {
  transition: <property> <duration> <timing-function> <delay>;
}

visibility: hidden - 
- occupies space
- not shown to user
- non-interactable: doesn't trigger on-hover when invisible 

display: none
- doesn't occupy space
- not shown to suer
- transition doesn't work well - since block removed from page, it cannot be partially displayed


opacity: 0
- occupies space (they are actually visible, just transparent)
- interactable: when hover over that invisible space, on-hover triggered. 
- doesn't trigger layout space

zIndex

height: 0

padding: x

https://www.freecodecamp.org/news/css-display-none-and-visibility-hidden-the-difference/