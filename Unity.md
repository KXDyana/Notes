# Unity
## windows
* project: resources
* scene: preview static
* game: preview dynamic
* hierarchy: objects in tree
* inspector: the attributes and properties of objects
* console: print code, for debug...

## Assets:
* texture: jpg/png...
* audioclip: mp3...
* c# script: *.cs
### Meta
*Every file and directories has a .meta file, descriping the object.

## Objects order:
* 2 ways to modify:
1. z axis 
2. order in layer

## Sprite Editor:
1. modify pivot
2. split multiple objects in one png file

## Component:
* every component has a feature
* eg: sprite renderer
### sprite renderer: display texture
### transform: basic component, modify position, rotation and scale of the object in the scene
### script: controls the behaviour of the gaming object

## order of execution
1. create all game objects in scene
2. create all components from game objects
* eg: Hand h1 = new Hand();
3. execute h1.Start();
4. execute h1.Update() every frame.

## frame rate
* frame rate is not fixed. 
* Time.deltaTime: time interval from last frame
* set frame rate (as close as possible): Application.targetFrameRate = 50;

## move game object:
```C#
Update(){
    this.transform.Translate(0, 0.05f, 0);
    //move up 0.05f per frame
}
```
* this.transform: transform component of this object owning the script
* Translate(): move position

However, the time interval is not fixed while the distance moved per time inverval is fixed. It would appears that the object is not moving in a constant speed. 

To fixed this:
```C#
Update(){
    float step = 0.8f * Time.deltaTime;
    this.transform.Translate(0, step, 0);
    //move up 0.8 unit per second
}
```
* the larger the time interval, the larger the moving distance
 
