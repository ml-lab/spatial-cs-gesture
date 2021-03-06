# Construction Mode - Gesture Ver.
**Author :** Yuan Yao  
**Last Update :** 2016.09.11

#### I. Introduction :
This is the gesture version of the game **Construction Mode**. It aims to help people practice their spatial reasoning skills. We used **Leap Motion** to detect the movement of user's hands and created a set of gestures as the input of the game.   
You can check the [demo](https://www.youtube.com/watch?v=Uku7eHwejqo) to briefly see how it works.

#### II. Operating Guide :
The set of gestures can be separated into two class : **one hand** and **two hands**. 

***Attention :*** The **one hand** class gesture ++only can be detected  when there is only one hand on the screen++, similarly **two hands** class gesture ++only can be detected when two hands appear on the screen++. The reason is because of the codes(HandController.cs) :

```C++
protected virtual void FixedUpdate()
{
    if (frame.Hands.Count == 2){
        ...
    }
    else if (frame.Hands.Count == 1){
        ...
    }
    else{
        ...
    }
}

```
Now here are the list of all the gestures.
#####  One Hand :  
1. **Swipe Gesture**  

Swipe your hand to rotate the object. The three direction are corresponding to three DoF of rotation. And the coordinate system is **Unity's coordinate system**. The difference between Leap Motion coordinate system and Unity system can seen as follows.  
**Leap Motion :** 
<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/leap-coordinate.png" alt="Drawing" style="height: 100px;"/>  

**Unity :** 
<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/unity-coordinate.png" alt="Drawing" style="height: 100px;"/>  

- Up or Down ( Swipe along with **Y-axis** ) : Clockwise ( direction > 0 ) or Counterclockwise ( direction < 0 ) rotation around **Z-axis**.  

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/swipe-y.png" alt="Drawing" style="height: 100px;"/>

- Left or Right ( Swipe along with **X-axis** ) : Clockwise ( direction < 0 ) or Counterclockwise ( direction > 0 ) rotation around **Y-axis**. 

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/swipe-x.png" alt="Drawing" style="height: 100px;"/>  

- Forward or Backward ( Swipe along with **Z-axis** ) : Clockwise ( direction < 0 ) or Counterclockwise ( direction > 0 ) rotation around **X-axis**. 

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/swipe-z.png" alt="Drawing" style="height:100px;"/>  

***Attention :*** ++All the swipe gestures should be parallel to the corresponding axis++ because of such codes :

```C++
if (
    (
    Math.Abs(swipe_direction_world.x) > 3 * Math.Abs(swipe_direction_world.y)
    ) && (
    Math.Abs(swipe_direction_world.x) > 3 * Math.Abs(swipe_direction_world.z)
    )
)

```
This condition sentence check whether your hand's movement is along the X-axis, therefore if the component of the movement on Y-axis or Z-axis is more that 1/3 of the component of that on X-axis, the movement won't be regarded as an X-axis swipe gesture. The swipe gestures on other directions are the same. To make it more generalizable, you can replace 3 with 2 or 1.5 .  



2. **Fist Gesture**

Make your hand become a feast and the object can move as long as your feast move.   

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/fist.png" alt="Drawing" style="height: 100px;"/>  

***Attention :*** Make sure **Leap Motion** can ++see all of your fingers++, for example do not do like this :

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/fist-error.png" alt="Drawing" style="height: 100px;"/>  



#####  Two Hands :

1. **Left Hand Fist Gesture**  

Make your left become a fist then you will enter selection mode which will call the menu.  

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/leftfist.png" alt="Drawing" style="height: 100px;"/>  

The actual result is as follow :

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/callmenu.png" alt="Drawing" style="height: 100px;"/>  

***Attention :*** To keep this menu, you should always keep your left hand as a fist and both of your two hands be presented on the screen.  

2. **Left Hand Fist Right Hand Swipe Gesture**  
 
Keep left hand as a fist and swipe your right hand, you will be able to make different objects highlighted.

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/select.png" alt="Drawing" style="height: 100px;"/>   

The actual result is as follow :

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/selectobject.png" alt="Drawing" style="height: 100px;"/>  

3. **Grab Gesture** 

Keep your two hands' fingers blending and move in the x-y plane, then the view will change as long as you move.  

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/grab-two.png" alt="Drawing" style="height: 100px;"/>  

The actual result is as follow :

<img src="https://github.com/rozentill/spatial-cs-gesture/blob/master/Assets/_Image/dragview.png" alt="Drawing" style="height: 100px;"/>  

***Attention :*** Grab gesture is different from fist, which means you should not blend your fingers too much. Also the directions of the movements of your hands should be the same.

<!--#### III. Implementation :-->