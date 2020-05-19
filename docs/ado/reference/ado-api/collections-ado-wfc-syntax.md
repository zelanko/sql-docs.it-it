---
title: Raccolte (sintassi ADO-WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
author: rothja
ms.author: jroth
ms.openlocfilehash: d5213e1c50f603663bb0405748f5dda882be5cfe
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748900"
---
# <a name="collections-ado---wfc-syntax"></a>Raccolte (sintassi ADO/WFC)
**pacchetto com. ms. wfc. Data**  
  
## <a name="parameters"></a>Parametri  
  
### <a name="methods"></a>Metodi  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>Campi  
  
### <a name="methods"></a>Metodi  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>Errori  
  
### <a name="methods"></a>Metodi  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
