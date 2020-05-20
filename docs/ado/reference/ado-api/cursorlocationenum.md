---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: rothja
ms.author: jroth
ms.openlocfilehash: 278f69e504ed4af7589b7e2be2c281e5de5957fa
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760177"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Specifica il percorso del servizio del cursore.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Utilizza cursori sul lato client forniti da una libreria di cursori locali. I servizi cursore locale spesso consentiranno numerose funzionalità che i cursori forniti dal driver non possono, pertanto l'utilizzo di questa impostazione può offrire un vantaggio rispetto alle funzionalità che verranno abilitate. Per compatibilità con le versioni precedenti, è supportato anche il sinonimo **adUseClientBatch** .|  
|**adUseNone**|1|Non utilizza i servizi Cursor. Questa costante è obsoleta e viene visualizzata esclusivamente per motivi di compatibilità con le versioni precedenti.|  
|**adUseServer come**|2|Valore predefinito. Utilizza i cursori forniti dal provider di dati o dal driver. Questi cursori sono a volte molto flessibili e consentono di aumentare la sensibilità delle modifiche apportate da altri utenti all'origine dati. Tuttavia, alcune funzionalità del [servizio Microsoft Cursor per OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), ad esempio dissociate<br /><br /> Gli oggetti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) non possono essere simulati con cursori sul lato server e queste funzionalità non saranno disponibili con questa impostazione.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. CursorLocation. CLIENT|  
|AdoEnums. CursorLocation. NONE|  
|AdoEnums. CursorLocation. SERVER|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
