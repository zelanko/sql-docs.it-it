---
title: Spazi dei nomi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5f28b5d593524288a755f4c9455bba39554d7bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924811"
---
# <a name="namespaces"></a>Spazi dei nomi
Il formato di persistenza XML in ADO utilizza i quattro spazi dei nomi seguenti.  
  
## <a name="remarks"></a>Osservazioni  
 Il formato di persistenza XML in ADO utilizza i quattro spazi dei nomi seguenti.  
  
|Prefisso|Descrizione|  
|------------|-----------------|  
|s|Si riferisce allo spazio dei nomi "XML-Data" contenente gli elementi e gli attributi che definiscono lo schema del recordset corrente.|  
|DT|Fa riferimento alla specifica delle definizioni dei tipi di dati.|  
|rs|Si riferisce allo spazio dei nomi contenente gli elementi e gli attributi specifici delle proprietà e degli attributi del recordset ADO.|  
|z|Si riferisce allo schema del set di righe corrente.|  
  
 Un client non deve aggiungere i propri tag a questi spazi dei nomi, come definito dalla specifica. Un client, ad esempio, non deve definire uno spazio dei nomi come "urn: schemas-microsoft-com: rowset", quindi scrivere qualcosa come "RS: MyOwnTag". Per ulteriori informazioni sugli spazi dei nomi, vedere la [raccomandazione W3C Namespaces in XML](http://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  L'ID del tag dello schema deve essere "RowsetSchema" e lo spazio dei nomi utilizzato per fare riferimento allo schema del set di righe corrente deve puntare a "#RowsetSchema".  
  
 Si noti che il prefisso dello spazio dei nomi, la parte tra i due punti e il segno di uguale, è arbitrario.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 L'utente può definire questa operazione come qualsiasi nome, purché questo nome venga usato in modo coerente in tutto il documento XML. ADO scrive sempre "s," "RS", "DT" e "z", ma questi nomi di prefisso non sono hardcoded nel componente di caricamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza di record in formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
