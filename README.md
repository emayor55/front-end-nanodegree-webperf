# How to run this application

1. Download the contents of this repository by cloning it. 
2. Locate the file named 'index.html'. 
3. Open the 'index.html' file using a browser by double-clicking on the file icon. 
(NOTE: If the default program that opens 'html' files on your computer is not a browser, you can open 'index.html' by right-clicking on the icon, locating the 'Open with...' option on the pop-up menu, and selecting a browser from the options provided) 
 
_______
###Optimizations implemented in views/js/main.js for pizza.html 

  ###A. How TIME to RESIZE PIZZAS was reduced to less than 5ms:
   The **_'changePizzaSizes()'_** method was refactored as follows: 
   * REMOVED the repeated execution of **_document.querySelectorAll(".randomPizzaContainer")_** from the **'for...loop'**. The method was being called 4 times for every iteration in the loop. This was unnecessary. The array of elements to be resized does not change, so executing this method once, outside of the **_'changePizzaSizes()'_** method itself, was all that was needed. 
   * REPLACED the method **_querySelectorAll()_** with the more efficient **_getElementsByClassName()_** operation.
   * REMOVED the unnecessary call to the **_determineDx()_** method which requires determining the **'offsetWidth'**, an operation that probably triggers layout. At the same time, this method performs a roundabout calculation that is totally unnecessary. Since each one of three possible values of the argument **'size'** maps to a specific **'newWidth'** value, there was no need for any calculation.  
   * USED the constant **100** (number of pizza containers, which is known), in the 'for...loop',  instead of constantly 'calculating' for the size of the array returned by the  **_getElementsByClassName()_** operation.  
 
   ________
  ###B. How FRAME RATE was increased to 60 FPS: 
1. The number of moving pizzas was reduced from 200 to 40, the maximum no. of pizza's visible on the screen anytime even at 50% display setting.
2. The method **_updatePositions()_** was refactored as follows: 
   * REPLACED the method **_querySelectorAll()_** with the more efficient **_getElementsByClassName()_** operation.
   *  MOVED the call to the **_getElementsByClassName('mover')_** method OUTSIDE of the **_updatePositions()_** method. There was no need to repeatedly call this method each time **_updatePositions()_** is executed.
   *  MOVED the calculation for the value of **document.body.scrollTop /1250** outside of ***'for..loop'***. This value does not vary for every animated pizza and is solely dependent on value of **'scrollTop'**. It does not have to be recalculated for every moving pizza.
   *  REPLACED the modulo operation **(i % 5 )** with an equivalent OUTER ***'for..loop'*** with 5 iterations, to calculate **'phase'** which at any **scrollTop** position can only have 5 possible values. 
   *  GROUPED the updates to the attribute **style.left** so that all animated pizzas to which a specific value of **'phase'** applies are updated one after another. 
   * ADDED the CSS3 attribute **"backface-visibility: hidden"** to the **.mover** class in **style.css**, to cause creation of separate layers for the animated pizzas, and thus reduce painting. 
________
  