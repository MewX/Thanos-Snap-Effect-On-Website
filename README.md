# Thanos-Snap-Effect-On-Website
# INTRODUCTION
What google did was that, they created multiple canvases that each one contain part of the original element. Then rotate and transform them until they fade away.
So with this concept, we’ll need to find a way to convert our element to image on canvas object. Then randomly distribute pixels from that image to multiple canvases. And finally add animation to each of them and hide the original element.
# First Step – Convert Element to Image.
We have a very useful library calls html2canvas. You can just pass any html element and it will return canvas object for you. Once we have included the library, we’ll pass our div element to get the canvas object. Then we’ll get an array containing all pixels data from it.
# Second Step – Chop Them to Pieces
We have the pixels array, we’ll try to distribute the pixels data to multiple canvases. Since we want the animation to start fading away from top to bottom, we need majority pixels at the top, to be in the first group of canvases & majority of bottom pixels in the last canvases group. This way, when we start each canvas’ animation sequentially , it will look like it’s fading from top to bottom.
The problem with this is that it is not a regular random anymore so we can’t just use Math.random . We create a weighted distribution function. Basically we’ll just increase the probability for the top pixels to be in the first canvases group and the bottom to be in the last. To achieve this, chance.js is used which is a JavaScript library dedicated for random utility.
Now we have the distributed pixels data. we’ll create canvases from them,and assign a class name. Then append them to the wrapper.
# Last Step – The Animation
The last step is to add the animation. First we’ll start fading away the original content using jQuery fadeout.
Then for each canvas, we’ll add three animations. First is blur. We add this to soften the transform or it will look pixelated. The second is transform. This is to move the pixels away from the original position. We add both rotation and translate using random value to simulate dust effect. And the third is fadeout to fade away the dust particle. JQuery doesn’t directly support blur or transform animation, so, you have to manually create a function for them.
# Style
On the CSS side There is nothing much. Just flex display to center everything and basic style for the snap button. The only thing related to the effect is the position absolute. This is to make all the canvases stay on the same position. The rest of the animation are handled by the JavaScript.
