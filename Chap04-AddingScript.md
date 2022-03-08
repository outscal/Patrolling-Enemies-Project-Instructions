# Adding Script

Ok, great job till now, let's get into the more spicy part of game development or programming.

![](https://media.giphy.com/media/13HgwGsXF0aiGY/giphy.gif)

You can create a new C# script in unity by right-clicking any folder in the Project structure 

![right_script](https://user-images.githubusercontent.com/44625252/154814427-39598bc8-d033-43bd-825d-c19779b3d3a6.png)

The name of the script will be the name of the class that woud be created using this.

So, let's think about this. The enemy needs to keep moving every frame using a speed value that can be input in the inspector. The following can be added in the script:

```
   public float speed;
   public float distance;
   private bool movingRight = true;
   public Transform groundDetection;
   
   private void Update()
   {
       transform.Translate(Vector2.right * speed * Time.deltaTime);
   }
```

For the next part, the enemy needs to change its direction of movement when it encounters the end of any platform. A very good use case here is of Raycasting. We can use another object within somehwere in the enemy object to send rays that hits downward.

Let's call this object 'Ground Detection'

![childRay](https://user-images.githubusercontent.com/44625252/154814674-ba264b5f-7494-41a7-89c7-ea66f95d5726.png)

Some lines in our script can be added to send rays downwards and check if the rays are touching a collider or not. If not, then we know that there is no other object down and the enemy movement can be triggered to change in opposite direction.

```
        RaycastHit2D groundInfo = Physics2D.Raycast(groundDetection.position, Vector2.down, distance);

        if (!groundInfo.collider)
        {
            if (movingRight)
            {
                transform.eulerAngles = new Vector3(0, -180, 0);
                movingRight = false;
            }
            else
            {
                transform.eulerAngles = new Vector3(0, 0, 0);
                movingRight = true;
            }
        }
```

What we are doing here, is change the rotation transform of the enemy to -180 or 0 based on the current direction of the enemy. The 'movingRight' variable is made to be true at start, hence, we should only place an enemy that is supposed to move to to the right, of course while placing itself then, the rotation can be changed to start enemy movement from right to left.

The code should be in the update() function as we want the change every frame. Remember to attach the script to the enemy gameobject for it to take place.

![Inspector_values](https://user-images.githubusercontent.com/44625252/154814800-d58e2271-4343-4274-b0f0-d83993e26a44.png)

Finally, if there are enemies that are crossing each other, then we can change the collision matrix value to 'disabled' for enemy->enemy collision.

![CollisionMatrixEnemy](https://user-images.githubusercontent.com/44625252/154815000-b6ed2480-735b-41ed-88a0-f3ab501f03a7.png)

Hope you enjoyed this. Feel free to try out different types of moving enemies for your game.

![](https://media.giphy.com/media/8VITX7wfegOSFWwnCH/giphy.gif)
