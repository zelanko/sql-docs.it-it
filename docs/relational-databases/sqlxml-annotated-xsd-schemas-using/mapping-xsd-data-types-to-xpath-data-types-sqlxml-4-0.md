---
title: Mapping dei tipi di dati XSD ai tipi di dati XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7f79a4d756a76dc6b59e76bbbfc28076ba36eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067056"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Mapping dei tipi di dati XSD ai tipi di dati XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando viene eseguita una query XPath su uno schema XSD e il tipo XSD è specificato nella **xsd: Type** attributo, XPath utilizza il tipo di dati specificato durante l'elaborazione della query.  
  
 Il tipo di dati XPath di un nodo viene derivato dal tipo di dati XSD nello schema, come illustrato nella tabella seguente. A scopo illustrativo, viene utilizzato il nodo EmployeeID.  
  
|Tipo di dati XSD|Tipo di dati XDR|Equivalente<br /><br /> Tipo di dati XPath|SQL Server<br /><br /> utilizzata|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**base64Binary**<br /><br /> **HexBinary**|**None**<br /><br /> **bin.base64bin.hex**|**Non applicabile**|Nessuna<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT(bit, EmployeeID)|  
|**Decimal, integer, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**numero, int, float, i1, i2, i4, i8, r4, r8ui1, ui2, ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**ID, idref, idrefsentity, entità, notation, nmtoken e nmtokens, DateTime, string, AnyURI**|**id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**Non applicabile (non vi è alcun tipo di dati in XPath è equivalente al tipo di dati XDR fixed14.4).**|CONVERT(money, EmployeeID)|  
|**data**|**data**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
