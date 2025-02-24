#sem6 #gamedevelopment #unity3D

## Basic Commands

1. In the Project Window, open Assets > Course Library > Vehicles, then drag a vehicle into the Hierarchy
2. Hold right-click + WASD to fly to the vehicle, then try to rotate around it
3. With the vehicle selected and your mouse in the Scene view, Press F to focus on it
4. Use the scroll wheel to zoom in and out and hold the scroll wheel to pan
5. Hold alt+left-click to rotate around the focal point or hold alt+right-click to zoom in and out
6. If anything goes wrong, press Ctrl/Cmd+Z to Undo until it’s fixed

## Shortcuts

![[Basics-1740245602245.webp]]

| Command | Bedeutung |
| ------- | --------- |
| Q       | View      |
| W       | Move      |
| E       | Rotate    |
| R       | Scale     |
| T       | Rect      |
| Y       | Transform |
## Code Example
### PlayerController

```cs
using UnityEngine;

  

public class PlayerController : MonoBehaviour

{

    // Private Variables
    private float speed = 20.0f;
    private float turnSpeed = 45.0f;
    private float horizontalInput;
    private float forwardInput;

    // Start is called before
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
        // This is where we get player input
        horizontalInput = Input.GetAxis("Horizontal");
        forwardInput = Input.GetAxis("Vertical");
  
        // We move the vehicle forward
        transform.Translate(Vector3.forward * Time.deltaTime * speed * forwardInput);
        // We turn the vehicle
        transform.Rotate(Vector3.up * Time.deltaTime * turnSpeed * horizontalInput);
    }
    
}
```

### FollowController

```cs
using UnityEngine;

public class FollowPlayer : MonoBehaviour
{

    public GameObject player;
    private Vector3 offset = new Vector3(0, 5, -7);

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {

    }

    // Update is called once per frame
    void LateUpdate()
    {
        // Offset the camera behind the player by adding to the player's position
        transform.position = player.transform.position + offset;
    }

}
```
