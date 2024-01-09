# Smart Floor Collider
[![Static Badge](https://img.shields.io/badge/Unity-2022.3.6f1-informational?style=flat&label=Unity)](https://unity.com/releases/editor/whats-new/2022.3.6)
[![Generic badge](https://img.shields.io/badge/SDK-AvatarSDK3-informational.svg)](https://vrchat.com/home/download)
[![Generic badge](https://img.shields.io/github/downloads/Zexxx/Smart-Floor-Collider/total?label=Downloads)](https://github.com/Zexxx/Smart-Floor-Collider/releases/latest)

Based on [World Constraint](https://github.com/VRLabs/World-Constraint).

It uses [VRCFury](https://vrcfury.com/) for fast installation.

## How to install it on your avatar
1. [Install the latest package](https://github.com/Zexxx/Smart-Floor-Collider/releases/latest)
2. [Install VRCFury](https://vrcfury.com/download/)
3. Drag and drop "Smart Floor Collider" onto the root of your avatar.
> [!NOTE]
> You must remove the old floor collider or move it to the "collider" game object located under the World Constraint. (If you are reparenting your own floor collider under the collider game object be sure to remove the physbone collider component from  "collider". 
4. VRFury should handle the rest. Click upload, and you are done.

## How it works
This works nearly identical to how [world constraints](https://github.com/VRLabs/World-Constraint/blob/main/README.md#how-it-works) normally work with a key few changes for this to work for this.

The first change is that the "World Constraint" only locks on the Y axis. Changing the Freeze Position Axis to only lock the Y axis allows the root parent constraint to follow us still around when it's holding an object in place. 

As a result, when you disable the child "Container" parent constraint, the object will stay in line with the avatar center but freeze in its last Y-axis position. 

For the FX Controller, to detect whether the user is on the ground, we use the [Global Parameter](https://creators.vrchat.com/avatars/animator-parameters/) "Grounded," when the user is not grounded, the "Container" parent constraint is disabled which causes the floor collider to instantly stop moving as soon as VRChat detects the local client is not on the ground. As soon as the avatar returns to the ground with Grounded = True, the "Container" parent constraint is enabled again. 

There is also a detection of whether the local client is falling with VelocityY. An issue with freezing the floor collider in place is being able to fall through it. The falling state aims to detect when the user is not Grounded and if VelocityY is less than -2. This disables the floor collider.
