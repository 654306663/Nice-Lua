# Camera Stacking
In the Universal Render Pipeline (URP), you use Camera Stacking to layer the output of multiple Cameras and create a single combined output. Camera Stacking allows you to create effects such as a 3D model in a 2D UI, or the cockpit of a vehicle.

![Camera Stacking in URP](Images/camera-stacking-example.png)

A Camera Stack consists of a [Base Camera](camera-types-and-render-mode.md#base-camera) and one or more [Overlay Cameras](camera-types-and-render-mode.md#overlay-camera). A Camera Stack overrides the output of the Base Camera with the combined output of all the Cameras in the Camera Stack. As such, anything that you can do with the output of a Base Camera, you can do with the output of a Camera Stack. For example, you can render a Camera Stack to a given render target, apply post-process effects, and so on.

You cannot apply post-processing to individual Overlay Cameras within a Camera Stack. You can apply post-processing to the Base Camera of a Camera Stack, which applies the effect to the combined output of the Camera Stack.

Unity does not perform any optimizations within a Camera Stack to prevent overdraw. When multiple Cameras in a Camera Stack render to the same render target, each pixel in the render target will be drawn for each Camera in the Camera Stack. For more information on overdraw in URP, see [Advanced information](cameras-advanced.md).

<a name=”adding-a-camera-to-a-camera-stack”></a>
## Adding a Camera to a Camera Stack

![Adding a Camera to a Camera Stack](Images/camera-stack-add-camera.png)

1. Create a Camera in your Scene. Its **Render Mode** defaults to **Base**, making it a Base Camera.
2. Create another Camera in your Scene, and select it. 
3. In the Camera Inspector, change the Camera’s  **Render Mode** to **Overlay**.
4. Select the Base Camera again. In the Camera Inspector, scroll to the Stack section, click the **plus (+)** button, and click the name of the Overlay Camera.

The Overlay Camera is now part of the Base Camera's Camera Stack. Unity renders the Overlay Camera's output on top of the Base Camera's output.

You can add a Camera to a Camera Stack in a script by directly manipulating the `cameraStack` property of the Base Camera's [UniversalAdditionalCameraData](../api/UnityEngine.Rendering.Universal.UniversalAdditionalCameraData.htmll) component, like this:

```
myBaseUniversalAdditionalCameraData.cameraStack.Add(myOverlayCamera);
```

## Removing a Camera from a Camera Stack

![Removing a Camera from a Camera Stack](Images/camera-stack-remove-camera.png)

1. Create a Camera Stack that contains at least one Overlay Camera. For instructions, see [Adding a Camera to a Camera Stack](#adding-a-camera-to-a-camera-stack).
2. Select the Camera Stack's Base Camera. 
3. In the Camera Inspector, scroll to the Stack section, click the name of the Overlay Camera you want to remove, and then click the **minus (-)** button.

The Overlay Camera remains in the Scene, but is no longer part of the Camera Stack.

You can remove a Camera from a Camera Stack in a script by directly manipulating the `cameraStack` property of the Base Camera's [UniversalAdditionalCameraData](../api/UnityEngine.Rendering.Universal.UniversalAdditionalCameraData.htmll) component, like this:

```
myBaseUniversalAdditionalCameraData.cameraStack.Remove(myOverlayCamera);
```

## Changing the order of Cameras in a Camera Stack

![Removing a Camera from a Camera Stack](Images/camera-stack-reorder.png)

1. Create a Camera Stack that contains more than one Overlay Camera. For instructions, see [Adding a Camera to a Camera Stack](#adding-a-camera-to-a-camera-stack).
2. Select the Base Camera in the Camera Stack. 
3. In the Camera Inspector, scroll to the Stack section. 
4. Use the handles next to the names of the Overlay Cameras to reorder the list of Overlay Cameras.

The Base Camera renders the base layer of the Camera Stack, and the Overlay Cameras in the stack render on top of this in the order that they are listed, from top to bottom.

You can reorder a Camera Stack in a script by directly manipulating the `cameraStack` property of the Base Camera's [UniversalAdditionalCameraData](../api/UnityEngine.Rendering.Universal.UniversalAdditionalCameraData.htmll) component.

## Adding the same Overlay Camera to multiple stacks

To add an Overlay Camera to multiple Camera Stacks:

1. Create a Camera Stack that contains at least one Overlay Camera. For instructions, see [Adding a Camera to a Camera Stack](#adding-a-camera-to-a-camera-stack).
2. Create a Camera in your Scene. Its **Render Mode** defaults to **Base**, making it a Base Camera.
3. Select the new Base Camera. 
4. In the Camera Inspector, scroll to the Stack section, click the *plus (+)* button, and click the name of the Overlay Camera that you want to use in both Camera Stacks.

The Overlay Camera is now rendering in both Camera Stacks.

You can also add a Camera to a Camera Stack in a script by directly manipulating the `cameraStack` property of the Base Camera's [UniversalAdditionalCameraData](../api/UnityEngine.Rendering.Universal.UniversalAdditionalCameraData.htmll) component, like this:

```
myBaseUniversalAdditionalCameraData.cameraStack.Add(myOverlayCamera);
```