#### while loop

```
var cards = ['Diamond', 'Spade', 'Heart', 'Club'];
var currentCard = 'Heart';

while (currentCard !== 'Spade') {
  
  var randomNumber = Math.floor(Math.random() * 4);
  
  currentCard = cards[randomNumber];
}

console.log('Found spade');
```

While current card is NOT equal to 'Spade' execute the code block below.  
Generate a random number then assign it as an index of `cards` array to the `currentCard` variable.  
Once currentCard matches 'Spade' move further to console.log  