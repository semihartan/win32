---
title: gluEndCurve function
description: The gluBeginCurve and gluEndCurve functions delimit a Non-Uniform Rational B-Spline (NURBS) curve definition.
ms.assetid: 'b00ec687-6127-4585-b7b7-06e8dca78cfc'
keywords: ["gluEndCurve function OpenGL"]
topic_type:
- apiref
api_name:
- gluEndCurve
api_location:
- Glu32.dll
api_type:
- DllExport
---

# gluEndCurve function

The [**gluBeginCurve**](glubegincurve.md) and **gluEndCurve** functions delimit a Non-Uniform Rational B-Spline ([NURBS](using-nurbs-curves-and-surfaces.md)) curve definition.

## Syntax


```C++
void WINAPI gluEndCurve(
  �GLUnurbs *nobj
);
```



## Parameters

<dl> <dt>

*nobj* 
</dt> <dd>

The NURBS object (created with [**gluNewNurbsRenderer**](glunewnurbsrenderer.md)).

</dd> </dl>

## Return value

This function does not return a value.

## Remarks

Use [**gluBeginCurve**](glubegincurve.md) to mark the beginning of a NURBS curve definition. After calling **gluBeginCurve**, make one or more calls to [**gluNurbsCurve**](glunurbscurve.md) to define the attributes of the curve. Exactly one of the calls to **gluNurbsCurve** must have a curve type of GL\_MAP1\_VERTEX\_3 or GL\_MAP1\_VERTEX\_4. To mark the end of the NURBS curve definition, call **gluEndCurve**.

OpenGL evaluators are used to render the NURBS curve as a series of line segments. Evaluator state is preserved during rendering with [**glPushAttrib**](glpushattrib.md) (GL\_EVAL\_BIT ) and [**glPopAttrib**](glpopattrib.md). For information on exactly what state these calls preserve, see **glPushAttrib**.

## Examples

The following functions render a textured NURBS curve with normals; texture coordinates and normals are also specified as NURBS curves:

``` syntax
gluBeginCurve(nobj); 
gluNurbsCurve(nobj, . . ., GL_MAP1_TEXTURE_COORD_2); 
gluNurbsCurve(nobj, . . ., GL_MAP1_NORMAL); 
gluNurbsCurve(nobj, . . ., GL_MAP1_VERTEX_4);  
gluEndCurve(nobj);
```

## Requirements



|                                     |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�2000 Professional \[desktop apps only\]<br/>                           |
| Minimum supported server<br/> | Windows�2000 Server \[desktop apps only\]<br/>                                 |
| Header<br/>                   | <dl> <dt>Glu.h</dt> </dl>     |
| Library<br/>                  | <dl> <dt>Glu32.lib</dt> </dl> |
| DLL<br/>                      | <dl> <dt>Glu32.dll</dt> </dl> |



## See also

<dl> <dt>

[**glPushAttrib**](glpushattrib.md)
</dt> <dt>

[**gluBeginSurface**](glubeginsurface.md)
</dt> <dt>

[**gluBeginTrim**](glubegintrim.md)
</dt> <dt>

[**gluNewNurbsRenderer**](glunewnurbsrenderer.md)
</dt> <dt>

[**gluNurbsCurve**](glunurbscurve.md)
</dt> </dl>

�

�




