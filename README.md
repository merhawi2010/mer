## Website Performance Optimization portfolio project

### Introduction 
This is the fifth project for [Front End Web Development Nano Degree](https://www.udacity.com/course/front-end-web-developer-nanodegree--nd001) at the Udacity. The main aim is to optimize the online portfolio and achieve a score of at least 90 ([pageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)) for both mobile and desktop users. Hence the critical rendering path was optimized using different techniques thought during the course.


### How to run the Portfolio 
The entire optimized portfolio is hosted at GitHub. The page can be accessed from [this link](https://merhawi2010.github.io). To inspect the code please clone the portfolio from my GitHub repository at  ```https://github.com/merhawi2010/merhawi2010.github.io.git```


#### Part 1: Optimize PageSpeed Insights score for index.html
Based on the recommendations of [pageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/), the index.html is optimized and the following changes were made.
1.	Irrelevant html Tages such as``` button, input, select, textarea, b, strong, pre, code, ol ```were removed from the style.css. In addition class level css selector was used hence codes such as header p span were replaced with classes css selector. 
2.	Css was minified using [cssminifier.com](https://cssminifier.com/) and completely in HTML inlined.
3.	Render blocking css and javaScripts were made to load asynchronously and were placed at the bottom of the HTML code. In addition to this media query was used to avoid unnecessary downloads during page load.
4.	Pizza.jpg was extremely large in size and inappropriate for a thumbnail. Hence it was reduced and compressed.

#### Part 2: Optimize Frames per Second in pizza.html
The ```views/pizza.html``` was optimized by modifying ```views/js/main.js``` in order to achieve at least 60 frames per second rate. The following changes were made:

1.	```updatePosition()``` was causing forced synchronous layout and hence was modified by removing the scrollTop variable outside the  forLoop. i.e
      ```     function updatePositions() {
              frame++;
              window.performance.mark("mark_start_frame");

              var items = document.querySelectorAll('.mover');
              var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
              for (var i = 0; i < items.length; i++) {
                var phase = Math.sin((scrollTop / 1250) + (i % 5));
                items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
              }
      ```


2.	The function ```determineDx (elem, size)``` contributes nothing to the pizza resizing and hence was removed. 
3.	```document.querySelectorAll(".randomPizzaContainer")``` was repeating itself and thus was stored under ```var randomPizza``` and was placed outside the forLoop.

           var randomPizza = document.querySelectorAll(".randomPizzaContainer");
              function changePizzaSizes(size) {
                for (var i = 0; i < randomPizza.length; i++) {
                  randomPizza[i].style.width = newSize + "%";
                }
              }
         
4.	The number of sliding pizzas were reduced from 200 to 27
