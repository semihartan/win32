---
title: Edge Detection Effect
description: Filters out the content of an image leaving lines at the edges of contrasting sections of the image.
ms.assetid: 'd22868cf-95fe-690e-66ac-268d7e116aee'
---

# Edge Detection Effect

Filters out the content of an image leaving lines at the edges of contrasting sections of the image.

The CLSID for this effect is CLSID\_D2D1EdgeDetection.

-   [Example Image](#example-image)
-   [Sample Code](#sample-code)
-   [Effect Properties](#effect-properties)
-   [Requirements](#requirements)
-   [Related topics](#related-topics)

## Example Image

![example of effect output](images/edge-detection-effect.png)

## Sample Code


```C++
ComPtr<ID2D1Effect> edgeDetectionEffect;
m_d2dContext->CreateEffect(CLSID_D2D1EdgeDetection, &amp;edgeDetectionEffect);
 
edgeDetectionEffect->SetInput(0, bitmap);
edgeDetectionEffect->SetValue(D2D1_EDGEDETECTION_PROP_STRENGTH, 0.5f);
edgeDetectionEffect->SetValue(D2D1_EDGEDETECTION_PROP_BLUR_RADIUS, 0.0f);
edgeDetectionEffect->SetValue(D2D1_EDGEDETECTION_PROP_MODE, D2D1_EDGEDETECTION_MODE_SOBEL);
edgeDetectionEffect->SetValue(D2D1_EDGEDETECTION_PROP_OVERLAY_EDGES, false);
edgeDetectionEffect->SetValue(D2D1_EDGEDETECTION_PROP_ALPHA_MODE, D2D1_ALPHA_MODE_PREMULTIPLIED);
 
m_d2dContext->BeginDraw();
m_d2dContext->DrawImage(edgeDetectionEffect.Get());
m_d2dContext->EndDraw();


```



## Effect Properties

The properties for the edge detection effect are defined by the [**D2D1\_EDGEDETECTION\_PROP**](d2d1-edgedetection-prop.md) enumeration.

## Requirements



|                          |                                                   |
|--------------------------|---------------------------------------------------|
| Minimum supported client | Windows 10 \[desktop apps \| Windows Store apps\] |
| Minimum supported server | Windows 10 \[desktop apps \| Windows Store apps\] |
| Header                   | d2d1effects\_2.h                                  |
| Library                  | d2d1.lib, dxguid.lib                              |



 

## Related topics

<dl> <dt>

[**ID2D1Effect**](id2d1effect.md)
</dt> </dl>

 

 



