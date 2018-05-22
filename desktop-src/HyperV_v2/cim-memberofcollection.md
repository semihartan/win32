---
Description: 'Represents a relationship in which a managed element is a member of and is aggregated by a collection.'
ms.assetid: '324284fa-ece6-41df-9891-040a7561dce4'
title: 'CIM\_MemberOfCollection class'
---

# CIM\_MemberOfCollection class

Represents a relationship in which a managed element is a member of and is aggregated by a collection.

## Syntax

``` syntax
[Association, Aggregation, Abstract, Version("2.6.0"), UMLPackagePath("CIM::Core::Collection"), AMENDMENT]
class CIM_MemberOfCollection
{
  CIM_Collection���� REF Collection;
  CIM_ManagedElement REF Member;
};
```

## Members

The **CIM\_MemberOfCollection** class has these types of members:

-   [Properties](#properties)

### Properties

The **CIM\_MemberOfCollection** class has these properties.

<dl> <dt>

**Collection**
</dt> <dd> <dl> <dt>

Data type: **CIM\_Collection**
</dt> <dt>

Access type: Read-only
</dt> <dt>

Qualifiers: [**Key**](https://msdn.microsoft.com/library/aa392157), [**Aggregate**](https://msdn.microsoft.com/library/aa393650)
</dt> </dl>

The collection that aggregates members.

</dd> <dt>

**Member**
</dt> <dd> <dl> <dt>

Data type: **CIM\_ManagedElement**
</dt> <dt>

Access type: Read-only
</dt> <dt>

Qualifiers: [**Key**](https://msdn.microsoft.com/library/aa392157)
</dt> </dl>

The member of the collection.

</dd> </dl>

## Requirements



|                                     |                                                                                                         |
|-------------------------------------|---------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�10 \[desktop apps only\]<br/>                                                             |
| Minimum supported server<br/> | Windows Server�2016<br/>                                                                          |
| Namespace<br/>                | Root\\virtualization\\v2<br/>                                                                     |
| MOF<br/>                      | <dl> <dt>WindowsVirtualization.V2.mof</dt> </dl> |
| DLL<br/>                      | <dl> <dt>Vmms.exe</dt> </dl>                     |



�

�



