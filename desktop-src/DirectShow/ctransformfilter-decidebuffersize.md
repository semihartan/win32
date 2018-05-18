---
Description: 'The DecideBufferSize method sets the output pin''s buffer requirements.'
ms.assetid: '33e41668-b4f6-4142-b22e-2ddfb96332df'
title: 'CTransformFilter.DecideBufferSize method'
---

# CTransformFilter.DecideBufferSize method

The `DecideBufferSize` method sets the output pin's buffer requirements.

## Syntax


```C++
virtual HRESULT DecideBufferSize(
  �IMemAllocator �������*pAlloc,
  �ALLOCATOR_PROPERTIES *ppropInputRequest
) = 0;
```



## Parameters

<dl> <dt>

*pAlloc* 
</dt> <dd>

Pointer to the [**IMemAllocator**](imemallocator.md) interface on the output pin's allocator.

</dd> <dt>

*ppropInputRequest* 
</dt> <dd>

Pointer to an [**ALLOCATOR\_PROPERTIES**](allocator-properties.md) structure that contains buffer requirements from the downstream input pin.

</dd> </dl>

## Return value

Returns S\_OK or another **HRESULT** value.

## Remarks

The output pin's [**CTransformOutputPin::DecideBufferSize**](ctransformoutputpin-decidebuffersize.md) method calls this method. The derived class must implement this method. For more information, see [**CBaseOutputPin::DecideBufferSize**](cbaseoutputpin-decidebuffersize.md).

## Requirements



|                    |                                                                                                                                                                                            |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>Transfrm.h (include Streams.h)</dt> </dl>                                                                                  |
| Library<br/> | <dl> <dt>Strmbase.lib (retail builds); </dt> <dt>Strmbasd.lib (debug builds)</dt> </dl> |



## See also

<dl> <dt>

[**CTransformFilter Class**](ctransformfilter.md)
</dt> </dl>

�

�



