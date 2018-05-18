---
title: Interfaces
description: This section describes the interfaces provided by the Microsoft DirectComposition \ 32;API.
ms.assetid: 'AE51F47F-4315-4DA2-959E-B256957BE6DA'
---

# Interfaces

This section describes the interfaces provided by the Microsoft DirectComposition API.

## In this section



| Topic                                                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**IDCompositionAffineTransform2DEffect**](idcompositionaffinetransform2deffect.md)<br/>     | The arithmetic composite effect is used to combine 2 images using a weighted sum of pixels from the input images. <br/>                                                                                                                                                                                                                                                                             |
| [**IDCompositionAnimation**](idcompositionanimation.md)<br/>                                 | Represents a function for animating one or more properties of one or more DirectComposition objects.<br/>                                                                                                                                                                                                                                                                                           |
| [**IDCompositionArithmeticCompositeEffect**](idcompositionarithmeticcompositeeffect.md)<br/> | The arithmetic composite effect is used to combine 2 images using a weighted sum of pixels from the input images.<br/>                                                                                                                                                                                                                                                                              |
| [**IDCompositionBlendEffect**](idcompositionblendeffect.md)<br/>                             | The Blend Effect is used to combine 2 images. <br/>                                                                                                                                                                                                                                                                                                                                                 |
| [**IDCompositionBrightnessEffect**](idcompositionbrightnesseffect.md)<br/>                   | The brightness effect controls the brightness of the image.<br/>                                                                                                                                                                                                                                                                                                                                    |
| [**IDCompositionColorMatrixEffect**](idcompositioncolormatrixeffect.md)<br/>                 | The color matrix effect alters the RGBA values of a bitmap.<br/>                                                                                                                                                                                                                                                                                                                                    |
| [**IDCompositionCompositeEffect**](idcompositioncompositeeffect.md)<br/>                     | The composite effect is used to combine 2 or more images. This effect has 13 different composite modes. The composite effect accepts 2 or more inputs. When you specify 2 images, destination is the first input (index 0) and the source is the second input (index 1). If you specify more than 2 inputs, the images are composited starting with the first input and the second and so on. <br/> |
| [**IDCompositionClip**](idcompositionclip.md)<br/>                                           | Represents a clip object that is used to restrict the rendering of a visual subtree to a rectangular area. <br/>                                                                                                                                                                                                                                                                                    |
| [**IDCompositionDesktopDevice**](idcompositiondesktopdevice.md)<br/>                         | An application must use the IDCompositionDesktopDevice interface in order to use DirectComposition in a Win32 desktop application. This interface allows the application to connect a visual tree to a window and to host layered child windows for composition<br/>                                                                                                                                |
| [**IDCompositionDevice**](idcompositiondevice.md)<br/>                                       | Serves as a factory for all other DirectComposition objects and provides methods to control transactional composition.<br/>                                                                                                                                                                                                                                                                         |
| [**IDCompositionDevice2**](idcompositiondevice2.md)<br/>                                     | Serves as a factory for all other DirectComposition objects and provides methods to control transactional composition.<br/>                                                                                                                                                                                                                                                                         |
| [**IDCompositionDevice3**](idcompositiondevice3.md)<br/>                                     | Serves as a factory for all other DirectComposition objects and provides methods to control transactional composition. <br/>                                                                                                                                                                                                                                                                        |
| [**IDCompositionDeviceDebug**](idcompositiondevicedebug.md)<br/>                             | Provides access to rendering features that help with application debugging and performance tuning. This interface can be queried from the DirectComposition device interface.<br/>                                                                                                                                                                                                                  |
| [**IDCompositionEffect**](idcompositioneffect.md)<br/>                                       | Represents a bitmap effect that modifies the rasterization of a visual's subtree. <br/>                                                                                                                                                                                                                                                                                                             |
| [**IDCompositionEffectGroup**](idcompositioneffectgroup.md)<br/>                             | Represents a group of bitmap effects that are applied together to modify the rasterization of a visual's subtree. <br/>                                                                                                                                                                                                                                                                             |
| [**IDCompositionFilterEffect**](idcompositionfiltereffect.md)<br/>                           | Represents a filter effect.<br/>                                                                                                                                                                                                                                                                                                                                                                    |
| [**IDCompositionFloodEffect**](idcompositionfloodeffect.md)<br/>                             | The flood effect is used to generate a bitmap based on the specified color and alpha value. You can use this effect when you want a specific color as an input for an effect, like a background color. <br/>                                                                                                                                                                                        |
| [**IDCompositionGaussianBlurEffect**](idcompositiongaussianblureffect.md)<br/>               |                                                                                                                                                                                                                                                                                                                                                                                                           |
| [**IDCompositionHueRotationEffect**](idcompositionhuerotationeffect.md)<br/>                 | The hue rotate effect alters the hue of an image by applying a color matrix based on the rotation angle. <br/>                                                                                                                                                                                                                                                                                      |
| [**IDCompositionLinearTransferEffect**](idcompositionlineartransfereffect.md)<br/>           | The linear transfer effect is used to map the color intensities of an image using a linear function created from a list of values you provide for each channel. <br/>                                                                                                                                                                                                                               |
| [**IDCompositionMatrixTransform**](idcompositionmatrixtransform.md)<br/>                     | Represents an arbitrary affine 2D transformation defined by a 3-by-2 matrix.<br/>                                                                                                                                                                                                                                                                                                                   |
| [**IDCompositionMatrixTransform3D**](idcompositionmatrixtransform3d.md)<br/>                 | Represents an arbitrary 3D transformation defined by a 4-by-4 matrix.<br/>                                                                                                                                                                                                                                                                                                                          |
| [**IDCompositionRectangleClip**](idcompositionrectangleclip.md)<br/>                         | Represents a clip object that restricts the rendering of a visual subtree to the specified rectangular region. Optionally, the clip object may have rounded corners specified.<br/>                                                                                                                                                                                                                 |
| [**IDCompositionRotateTransform**](idcompositionrotatetransform.md)<br/>                     | Represents a 2D transformation that affects the rotation of a visual around the z-axis. The coordinate system is rotated around the specified center point. <br/>                                                                                                                                                                                                                                   |
| [**IDCompositionSaturationEffect**](idcompositionsaturationeffect.md)<br/>                   | This effect is used to alter the saturation of an image. The saturation effect is a specialization of the�color matrix�effect. <br/>                                                                                                                                                                                                                                                                |
| [**IDCompositionRotateTransform3D**](idcompositionrotatetransform3d.md)<br/>                 | Represents a 3D transformation that affects the rotation of a visual along an arbitrary axis in 3D space. The coordinate system is rotated around the specified center point. <br/>                                                                                                                                                                                                                 |
| [**IDCompositionScaleTransform**](idcompositionscaletransform.md)<br/>                       | Represents a 2D transformation that affects the scale of a visual along the x-axis and y-axis. The coordinate system is scaled from the specified center point. <br/>                                                                                                                                                                                                                               |
| [**IDCompositionScaleTransform3D**](idcompositionscaletransform3d.md)<br/>                   | Represents a 3D transformation effect that affects the scale of a visual along the x-axis, y-axis, and z-axis. The coordinate system is scaled from the specified center point. <br/>                                                                                                                                                                                                               |
| [**IDCompositionSkewTransform**](idcompositionskewtransform.md)<br/>                         | Represents a 2D transformation that affects the skew of a visual along the x-axis and y-axis. The coordinate system is skewed around the specified center point. <br/>                                                                                                                                                                                                                              |
| [**IDCompositionShadowEffect**](idcompositionshadoweffect.md)<br/>                           | The shadow effect is used to generate a shadow from the alpha channel of an image. The shadow is more opaque for higher alpha values and more transparent for lower alpha values. You can set the amount of blur and the color of the shadow. <br/>                                                                                                                                                 |
| [**IDCompositionSurface**](idcompositionsurface.md)<br/>                                     | Represents a physical bitmap that can be associated with a visual for composition in a visual tree. This interface can also be used to update the bitmap contents. <br/>                                                                                                                                                                                                                            |
| [**IDCompositionTableTransferEffect**](idcompositiontabletransfereffect.md)<br/>             | The table transfer effect is used to map the color intensities of an image using a transfer function created from interpolating a list of values you provide.<br/>                                                                                                                                                                                                                                  |
| [**IDCompositionSurfaceFactory**](idcompositionsurfacefactory.md)<br/>                       | Creates surface and virtual surface objects associated with an application-provided rendering device.<br/>                                                                                                                                                                                                                                                                                          |
| [**IDCompositionTarget**](idcompositiontarget.md)<br/>                                       | Represents a binding between a DirectComposition visual tree and a destination on top of which the visual tree should be composed. <br/>                                                                                                                                                                                                                                                            |
| [**IDCompositionTransform**](idcompositiontransform.md)<br/>                                 | Represents a 2D transformation that can be used to modify the coordinate space of a visual subtree. <br/>                                                                                                                                                                                                                                                                                           |
| [**IDCompositionTransform3D**](idcompositiontransform3d.md)<br/>                             | Represents a 3D transformation effect that can be used to modify the rasterization of a visual subtree. <br/>                                                                                                                                                                                                                                                                                       |
| [**IDCompositionTranslateTransform**](idcompositiontranslatetransform.md)<br/>               | Represents a 2D transformation that affects only the offset of a visual along the x-axis and y-axis.<br/>                                                                                                                                                                                                                                                                                           |
| [**IDCompositionTurbulenceEffect**](idcompositionturbulenceeffect.md)<br/>                   | The turbulence effect is used to generate a bitmap based on the Perlin noise function. The turbulence effect has no input image. <br/>                                                                                                                                                                                                                                                              |
| [**IDCompositionTranslateTransform3D**](idcompositiontranslatetransform3d.md)<br/>           | Represents a 3D transformation that affects the offset of a visual along the x-axis, y-axis, and z-axis. <br/>                                                                                                                                                                                                                                                                                      |
| [**IDCompositionVirtualSurface**](idcompositionvirtualsurface.md)<br/>                       | Represents a sparsely allocated bitmap that can be associated with a visual for composition in a visual tree.<br/>                                                                                                                                                                                                                                                                                  |
| [**IDCompositionVisual**](idcompositionvisual.md)<br/>                                       | Represents a DirectComposition visual. <br/>                                                                                                                                                                                                                                                                                                                                                        |
| [**IDCompositionVisual2**](idcompositionvisual2.md)<br/>                                     | Represents one DirectComposition visual in a visual tree.<br/>                                                                                                                                                                                                                                                                                                                                      |
| [**IDCompositionVisual3**](idcompositionvisual3.md)<br/>                                     | Represents one DirectComposition visual in a visual tree.<br/>                                                                                                                                                                                                                                                                                                                                      |
| [**IDCompositionVisualDebug**](idcompositionvisualdebug.md)<br/>                             | Represents a debug visual.<br/>                                                                                                                                                                                                                                                                                                                                                                     |



�

## Related topics

<dl> <dt>

[DirectComposition Reference](reference.md)
</dt> </dl>

�

�




