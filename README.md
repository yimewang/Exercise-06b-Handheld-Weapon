# Exercise-06b-Handheld-Weapon

Exercise for MSCH-C220

A demonstration of this exercise is available at [https://youtu.be/QyioUMnDEok](https://youtu.be/QyioUMnDEok)

This exercise explores attaching models together, preserving their animation. We will be working with a (slightly) modified version of the [3D-Character](https://github.com/BL-MSCH-C220/3D-Character).

Fork this repository. When that process has completed, make sure that the top of the repository reads [your username]/Exercise-06b-Handheld-Weapon. Edit the LICENSE and replace BL-MSCH-C220 with your full name. Commit your changes.

Clone the repository to a Local Path on your computer.

Open Godot. Import the project.godot file and open the "Handheld Weapon" project.

In res://Game.tscn, I have provided a starting place for the exercise: the scene contains a parent Spatial node (named Game) and a StaticBody Ground node (containing a MeshInstance Plane and a CollisionShape). There is a light source and a camera. The character model has been instanced. We will now add a blaster into the hand of the character.

First, download the [Blaster Kit](https://kenney.nl/assets/blaster-kit) 3D assets from kenney.nl. Unzip the file, and then copy the blasterJ.glb model from the Models/GLTF format folder into the Assets folder for this project. You should receive an indication in Godot that the model is being imported.

In the Godot FileSystem panel, open res://Assets/blasterJ.glb. When you are presented with the warning message, select "New Inherited". You should now see the blaster model in a new scene.

We need to modify the blaster slightly to make it easier to line it up in the character's hand:
 - Rename the root node "Blaster"
 - Rotate the Blaster node by 180 degrees in the y axis
 - Scale the Blaster node (in all three dimensions) to 1.5
 - Translate the Blaster node to x = -0.225, y = 0.08, z = -0.5

Then save the scene as res://Player/Blaster.tscn

Open the res://Player/Player.tscn scene.

Select the AnimationTree node and set Active = off.

Right-click on the Skeleton node, and Add Child Node. Select a BoneAttachment. After selecting the new BoneAttachment node, in the Inspector, choose right_hand_thumb_1 as the Bone Name.

As a child on the BoneAttachment node, Instance Child Scene and select res://Player/Blaster.tscn (*not res://Assets/blasterj.gbl!*). The blaster should appear near the Character's hand. We just have to move it into the right place:
 - Rotate the Blaster node: x = -38, y = -148, z = -1.6
 - Translate the Blaster node to x = -0.45, y = 0.45, z = -0.26

Finally, attach a script the the Player node (save it as res://Player/Player.gd):

```
extends KinematicBody

func _physics_process(_delta):
	if not $AnimationPlayer.is_playing():
		$AnimationTree.active = true
		
	if Input.is_action_just_pressed("shoot"):
		$AnimationTree.active = false
		$AnimationPlayer.play("Shoot")
```

Save the scene and return to res://Game.tscn. Run the scene. You should see the Character raise and shoot the gun when you press space bar. In the future, you may want to add a muzzle flash or other effects (or sound!) to reinforce the fact the gun is being fired.

Quit Godot. In GitHub desktop, add a summary message, commit your changes and push them back to GitHub. If you return to and refresh your GitHub repository page, you should now see your updated files with the time when they were changed.

Now edit the README.md file. When you have finished editing, commit your changes, and then turn in the URL of the main repository page (https://github.com/[username]/Exercise-06b-Handheld-Weapon) on Canvas.

The final state of the file should be as follows (replacing the "Created by" information with your name):

```
# Exercise-06b-Handheld-Weapon

Exercise for MSCH-C220

A simple example of an animated character with a hand-held weapon. Press space to fire.

## Implementation

Built using Godot 3.5

## References
 - Based on the [Kenney Character Assets](https://kenney.itch.io/kenney-character-assets) provided by kenney.nl. The model and animations were compiled in Blender and then imported into Godot.
 - [Blaster Kit](https://kenney.nl/assets/blaster-kit) from Kenney.nl

## Future Development

Muzzle flash or other effects

## Created By

Jason Francis
```
