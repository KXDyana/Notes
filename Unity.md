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
GameObject parent = this.transform.parent.gameObject;
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
```C#
GameObject obj3 = GameObject.find("lost equipment");
obj3.transform.SetParent(null);
//set obj3's parent as the scene/root object
```

## attributes of component
```C#
* public * = *;
```

## movement calculation
* position: Vector3 (x,y,z) 
```C#
transform.position
```
* rotation: Vector3
```C#
transform.eulerAngles
// or use transform.rotation, Vector4. more complicated
// positive: counterclockwise
``` 
position/rotation can be local or worldspace:
```C#
transform.localPosition
transform.localEulerAngles
```

## continuous movement
```C
transform.Translate(0,0.02f,0,Space.Self);
//Space.Self: refer oneself to move
//Space.World: refer the scene to move
```

## Vector
* to get the magnitude (length of a vector):
```C#
float len = v.magnitude;
```
* to normalize a vector (change the length to 1)
```C#
Vector3 normalizedV = v.normalized
```
* static constant:
```C#
Vector3.right = (1,0,0)
Vector3.up = (0,1,0)
Vector3.forward = (0,0,1)
```
* printing vector: default only one decimal. to print more, use
```C#
v.ToString("F3");
```

## Vector Calculation
* addition (subtraction):
```
(a,b) + (c,d) = (a + c, b + d)
```
* multiplication by constant
```
3(a, b) = (3a, 3b)
```
* dot multiplication
```

```
* cross multuiplication
```

```

### eg: calculate distance
```C#
GameObject target = GameObject.Find("targetObj");
Vector3 targetPosition = target.transform.position;
Vector3 selfPosition = this.transform.position;

Vector direction = targetPosition - selfPosition;
Debug.Log("distance between self and target = " + direction.magnitude);
```

### calculate angle
* to get the angle between two vectors:
```C#
Vector3 a = new Vector3(2,2,0);
Vector3 b = new Vector3(-1,3,0);
float angle = Vector3.SignedAngle(a, b, Vector3.forward);
//counterclockwise: positive; clockwise: negative
```

* direction of an object
```C#
transform.right: the X axis of the object
transform.up: the Y axis of the object
transform.forward: the Z axis of the object
this.transform.rotate
```

## coordinates
* scene coordinate
* screen coordinate
    * Screen.width (pixel)
    * Screen.height
```C#
Vector3 screenPos = camera.main.WorldToScreenPoint(worldPos);
```

## player boundarie: use screen coordinate

## event functions
* starting with "On", triggered when corresponding event occurs
* not starting with "On", automatically triggered by system.
* e.g.:
    * OnAwake: when instance is created
    * OnEnable: when component is enabled
    * if disabled, only Awake() is executed.

## ordering of function exeuction
```C#
for (Script s: sss){
    s.Awake();
}
for (Script s: sss){
    s.Start();
}
```
* no obvious ordering of which object is executed first
* if some script need to be executed first, use execution order:

## Mouse Event
* In Update(), we can detect mouse event
```C#
if(Input.GetMouseButtonDown(0)){ //0: left, 1: right, 2: wheel
    Debug.Log("Pressed at " + Input.mousePosition);
}
```

## Prefab
* previously created, used for dynamicly creating objs
* override -> apply all: apply changes to prefab and other instances
* unpack prefab: unlink linkage between instance and prefab

## dynamically creating prefab:
```C#
public GameObject myPrefab;
// link in inspector

GameObject bullet = Instantiate(myPrefab);//new bullet
bullet.transform.position = transform.position + new Vector3 (0,1f,0);// place above the plane
bullet.name = "my bullet";
```
## dynqamically destroy obj:
```C#
Destroy(this.GameObject);
```

## Timer
```C#
private float interval = 0.4f;
private float count = 0;


void Update(){
    count += Time.deltaTime();
    if (count >= interval){
        count = 0;
        Fire();
    }
}
```

## Keyboard Event
```
Input.GetKeyDown(key);
Input.GetKeyUp(key);
Input.GetKey(key);//get state
```

## physics
* RigidBody: has mass, velocity...
    types:
    * dynamic: has mass, has velocity
    * static: infinite mass, 0 velocity (typically on buildings)
    * kinematic: 0 mass

## collision
* collider component
## Bounce:
* create physics material
    * friction
    * bounciness
* rigidbody-material

## Kinematic Rigidbody
* used for collision detection 
* In collider component, check istrigger
* 
```C#
private void OnTriggerEnter2D(Collider2D collision){
    //collision: the colliding object component
    collision.gameObject 
    collision.transform
    collision.name
    sollicion.tag

}
// what happens when collisions start, happens once
private void OnTriggerStay2D(Collider2D collision){

}
//what happens when collision is happending, happens every frame

private void OnTriggerExit(Collider2D collision){

}
// what happens when collision ends, happens once.
```

## Collision detection
* tag: player/enemy
```C# 
private void OnTriggerEnter(Collider2D collision){
    if(collision.gameObject.tag.Equals("Enemy")){
        Destroy(collision.gameObject);
    }
}
```

## avoid collision detection (for performance)
* use layers&layer collision matrix: collisions between some layers can be ignored

## Centre Controller
* MyGame.cs: for global settings (such as Application.targetFrameRate)

## repeated creating objects
```C#
float spawnYPosition = Random.Range(min,max);
void Start(){
    InvokeRepeating("CreateMonster", 0.1f, 2f);
}
```

## use multiple sprites for enemy
```C#
Sprite[] images;
void CreateMonster(){
    float monsterX = Random.Range(-2,2);
    float monsterY = 5;
    GameObject monster = Instantiate(monsterPrefab);
    monster.transform.position = new Vector(monsterX,monsterY,0);

    int index = Random.Rnage(0, images.Length);
    SpriteRenderer renderer = monster.GetComponent<SpriteRenderer>();
    renderer.sprite = this.images[index];

    //scale monster
    Sprite sprite = this.image[index];
    float imgWidth = sprite.rect.width;
    float scale = 100 / imgWidth;
    monster.transform.localScale = new Vector3(scale,scale,scale);
}
```


## Backgound Crontroller
* use two (or more) images to create a looping background
```C#
public class BackgroundCtrl : MonoBehaviour{
    Transform bg1;
    Transform bg2;
    // since we are only using Transform Component, we dont need the GameObj

    void Start(){
        bg1 = GameObject.Find("bg/bg1").transform;
        bg2 = GameObject.Find("bg/bg2").transform;

        bg1.position = new Vector3(0,0,0);
        bg2.position = new Vector3(0,10,0);


    }

    void Update(){
        float dy = speed * Time.deltaTime;
        bg1.Translate(0, -dy, 0);
        bg2.Translate(0, -dy, 0);

        if (bg1.position.y <= -10){
            bg1.Translate(0,20,0);
        }
        if (bg2.position.y <= -10){
            bg2.Translate(0,20,0);
        }
    }
}
```

## play audio
```C# 
AudioSource audio = GetComponent<AudioSource>();
audio.PlayOneShot(audio.clip);  //not overplay
audio.Play();                   //overplay
```

## Delayed execution
Invoke("Reponse", 3);

## Scoring
* using main controller
```C#
public class MyGame : MonoBehaviour{
    public int score = 0;

    void Start(){

    }
    void Update(){

    }
    public void AddScore(int value){
        this.score += value;   
    }
}
```
```C#
public class Mole:MonoBehaviour{
    Update(){
        if (hit()){
            GameObject main = GameObject.Find("main_controller");
            MyGame myGame = main.GetComponent<MyGame>();
            myGame.AddScore(1);

            //main.SendMessage("AddScore",1);
            //same effect
        }
    }
}
```
