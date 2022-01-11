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
* this way, the larger the time interval, the larger the moving distance, creating an illution of constant speed

## get other components under the same game object
```C#
SpriteRenderer renderer = this.gameObject.GetComponent<SpriteRenderer>();
SpriteRenderer renderer = this.GetComponent<SpriteRenderer>();
SpriteRenderer renderer = GetComponent<SpriteRenderer>();
//all functions the same way
```
## get other game object under the same scene
```C#
GameObject obj1 = GameObject.Find("/Figure/22");
SpriteRenderer renderer2 = obj1.GetComponent<SpriteRenderer>();
renderer2.flipY = true;
```
## Parend and Child
* mained by Transform Component
* To get the parent object of current object:
```C#
GameObject parent = this.Transform.parent.gameObject;
```
* To get the child objects of current object:
```C#
foreach(Transform child in transform){
    Debug.log("I am child " + child.name);
}
```

## modify object hierachy
```C#
GameObject obj1 = GameObject.find("plane");
GameObject obj2 = GameObject.find("summoner");
obj1.transform.SetParent(obj2.transform);
//set obj1 as a child of obj2
```
 
