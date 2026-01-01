# Creating Custom Unity Project Templates
Instructions for creating custom project templates for the unity game engine. Ex: "Universal 2D", "Universal 3D" \
Accurate as of 12/13/2025 Unity Version 6000.2.6f2. \
This guide is written for Windows.

# Quick Overview
Have you ever wished you didn't need to delete the same unused packages 
over and over again when starting a new project? Or just wanted to have the tools you always use
to already be imported? \
Well now you can! This guide will show you how to change the default packages installed on new Unity projects.
You can also change the versions of the packages so you don't have to keep updating them :D

1. Copy an existing Project Template to use as a base.
2. Extract the copied folder and edit the "project.manifest".
3. Recompress and copy the new custom template into the \[EditorVersion]...\ProjectTemplates folder.
4. Relaunch the hub and use the new custom template.

# Step 1: Find the Built-in Templates

1. Go to the following path: \
   C:\Program Files\Unity\Hub\Editor\[YourEditorVersion]\Editor\Data\Resources\PackageManager\ProjectTemplates
2. Inside the ProjectTemplates folder you will find compressed folders that are named something like "com.unity.template.3d-7.0.1.tgz".
3. Copy the one you would like to use as a base into a separate location.

# Step 2: Extract contents and edit "project.manifest".
1. Extract the copied folder and open it; you will find another compress folder inside a ".tar".
2. Extract the second folder and open it; inside you will find a folder named "package" which holds the contents of the template.
3. Open the "project.manifest" file which is located at the root of the "package" folder. \
The contents of the "project.manifest" will look something like this

```
{
  "dependencies": {
    "com.unity.collab-proxy": "2.6.0",
    "com.unity.2d.animation": "10.1.4",
    "com.unity.2d.psdimporter": "10.0.0",
    "com.unity.2d.sprite": "1.0.0",
    "com.unity.2d.spriteshape": "10.0.7",
    "com.unity.2d.tilemap": "1.0.0",
    "com.unity.2d.tilemap.extras": "4.2.1",
    "com.unity.2d.aseprite": "1.2.1",
    "com.unity.ide.rider": "3.0.34",
    "com.unity.ide.visualstudio": "2.0.22",
    "com.unity.inputsystem": "1.12.0",
    "com.unity.render-pipelines.universal": "17.0.3",
    "com.unity.test-framework": "1.4.5",
    "com.unity.timeline": "1.8.7",
    "com.unity.ugui": "2.0.0",
    "com.unity.visualscripting": "1.9.5"
  },
  "description": "This is an empty project configured for 2D apps. It uses Unity’s Universal Render Pipeline pre-configured with 2D Renderer.",
  "displayName": "Universal 2D",
  "host": "hub",
  "name": "com.unity.template.universal-2d",
  "type": "template",
  "unity": "6000.1",
  "unityRelease": "0b1",
  "version": "6.1.1",
  "_upm": {
    "changelog": "### Changed\n- Set Quality -> Render Pipeline Asset in all quality levels and remove Default Render Pipeline setting from Graphics"
  },
  "upmCi": {
    "footprint": "8de2d61d5969336a56f4219fe1998fb38761a72d"
  },
  "repository": {
    "url": "https://github.cds.internal.unity3d.com/unity/2d.git",
    "type": "git",
    "revision": "1eb5a081fbd4f469011bf9ecfded9e2fb1269173"
  }
}
```
# Step 3: Compress And Put Back Into \[EditorVersion]...\ProjectTemplates 
1. Save your changed to the package.manifest file
2. Compress the inner folder and the outer folders back into .tar achives using a tool like [7-zip](https://www.7-zip.org/)
3. Place back into C:\Program Files\Unity\Hub\Editor\[YourEditorVersion]\Editor\Data\Resources\PackageManager\ProjectTemplates

And your Done :D
Open up Unity Hub and look for your new template when creating a project with the specified unity version.

## Understanding the "project.manifest" file

This is just a quick overview of the key things to know in this file, 
if you wish to read more you can refer to the official Unity documentation https://github.com/Mateo-Jimenez76/Creating-Custom-Unity-Project-Templates/edit/main/README.md

### "dependencies"

This section relates to Unity Packages to install automatically upon project creation.
For example the `"com.unity.inputsystem": "1.12.0"` line explains to install the package titled "com.unity.inputsystem" with the version 1.12.0.
To read more about package naming refer to the official Unity package name guidelines https://docs.unity3d.com/Manual/cus-naming.html

I imagine that linking a github repository as a dependency would work although I havent tested it. 
For more info on how to do this refer to the official documentation https://docs.unity3d.com/Manual/upm-git.html


### "displayName" vs "name"

DisplayName \
This name will appear in the Unity Hub when selecting a project template
> A user-friendly name that appears in the Unity Editor (for example, in the Project window, the Package Manager window, etc.).

Name

> [!WARNING]
> This name must match exactly with the name of the parent folder, and yes it is case sensitive. If names dont match then it wont be loaded.

> A unique identifier that conforms to the Unity Package Manager naming convention, which uses reverse domain name notation.

Quotes taken from the Unity documentation https://docs.unity3d.com/6000.0/Documentation/Manual/upm-manifestPkg.html

### "unity"/"unityRelease"/"version" whats the difference?

"unity": "6000.1", The project template was created for Unity editor version 6000.1 \
"unityRelease": "0b1", The specific patch/hotfix that the template was created for, in this case 6000.1.0b1 \
"version": "6.1.1", The version of the template. \
You will never need to change these values as they are purely for backend development.
