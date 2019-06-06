---
title: CommandTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommandTypeEnum
helpviewer_keywords:
- CommandTypeEnum enumeration [ADO]
ms.assetid: 4b1feb9c-a855-40fe-a906-efe688687e9f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 09874df6d9e09da8b6dc0df3e9670e4ff130c511
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695975"
---
# <a name="commandtypeenum"></a>CommandTypeEnum
Specifica come deve essere interpretato un argomento di comando.  
  
 È importante convalidare fornito dall'utente *CommandString* i valori per evitare che gli utenti dell'applicazione la possibilità di inserire comandi potenzialmente pericolosi per ADO per l'esecuzione.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adCmdUnspecified**|-1|Non specifica l'argomento di tipo di comando.|  
|**adCmdText**|1|Viene valutata [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) come una definizione testuale di un comando o stored procedure chiamata.|  
|**adCmdTable**|2|Viene valutata **CommandText** come un nome di tabella le cui colonne vengono restituite da una query SQL generata internamente.|  
|**adCmdStoredProc**|4|Viene valutata **CommandText** come un nome di stored procedure.|  
|**adCmdUnknown**|8|Valore predefinito. Indica che il tipo di comando in di **CommandText** proprietà non è noto.<br /><br /> Quando il tipo di comando non è noto, ADO farà numerosi tentativi per interpretare la **CommandText**.<br /><br /> -   **CommandText** viene interpretato come una definizione di testuale di una chiamata di comando o stored procedure. Si tratta dello stesso comportamento **adCmdText**.<br />-   **CommandText** è il nome di una stored procedure. Si tratta dello stesso comportamento **adCmdStoredProc**.<br />-   **CommandText** viene interpretato come il nome di una tabella. Vengono restituite tutte le colonne da una query SQL generata internamente. Si tratta dello stesso comportamento **adCmdTable**.|  
|**adCmdFile**|256|Viene valutata **CommandText** come nome del file di un oggetto archiviato in modo permanente [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Utilizzato con **Recordset.** [Aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) oppure [Requery](../../../ado/reference/ado-api/requery-method.md) solo.|  
|**adCmdTableDirect**|512|Viene valutata **CommandText** come un nome di tabella le cui colonne vengono restituiti. Utilizzato con **Open** oppure **Requery** solo. Usare la [Seek](../../../ado/reference/ado-api/seek-method.md) metodo, il **Recordset** deve essere aperta con **adCmdTableDirect**.<br /><br /> Questo valore non può essere combinato con il [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valore **adAsyncExecute**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.CommandType.UNSPECIFIED|  
|AdoEnums.CommandType.TEXT|  
|AdoEnums.CommandType.TABLE|  
|AdoEnums.CommandType.STOREDPROC|  
|AdoEnums.CommandType.UNKNOWN|  
|AdoEnums.CommandType.FILE|  
|AdoEnums.CommandType.TABLEDIRECT|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà CommandType (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)|[Metodo Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Metodo Execute (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|[Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Metodo Requery](../../../ado/reference/ado-api/requery-method.md)||
