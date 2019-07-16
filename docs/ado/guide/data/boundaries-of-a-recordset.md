---
title: Limiti di un Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f4efddad1b55ce57c62ce52418539ec06599bb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925916"
---
# <a name="boundaries-of-a-recordset"></a>Limiti di un recordset
**Recordset** supporta la **BOF** e **EOF** le proprietà per delineare l'inizio e alla fine, rispettivamente, del set di dati. È possibile pensare **BOF** e **EOF** come record "fittizio" che vengono posizionati all'inizio e alla fine del **Recordset**. Il conteggio **BOF** e **EOF**, un campione **Recordset** sarebbe simile al seguente:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|PROPRIETÀ BOF|||  
|7|Secca biologica frutta|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle rossi|45.6000|  
|51|Manjimup secchi mele|53.0000|  
|74|Tofu a lunga conservazione|10.0000|  
|EOF|||  
  
 Quando un cursore si sposta oltre l'ultimo record **EOF** è impostata su **True**; in caso contrario, il relativo valore è **False**. Analogamente, quando il cursore si sposta prima del primo record **BOF** è impostata su **True**; in caso contrario, il relativo valore è **False**. Queste proprietà vengono comunemente utilizzate per enumerare i record nel set di dati, come illustrato nel seguente frammento di codice JScript.  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 Se entrambe **BOF** e **EOF** sono **True**, il **Recordset** oggetto è vuoto. Entrambe le proprietà saranno **False** per appena aperto, non vuoti **Recordset** oggetto. È possibile usare la **BOF** e **EOF** delle proprietà per determinare se un **Recordset** oggetto è vuoto o non, come illustrato nel seguente frammento di codice JScript.  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 Questo schema funziona per tutti i tipi di cursore ed è indipendente dal provider sottostante. Se si tenta di determinare il contenuto di un **Recordset** oggetto controllando se relativi **RecordCount** valore della proprietà è zero (0) o No, è necessario adottare alcune precauzioni per utilizzare un cursore appropriato e un provider che supporta la restituzione del numero di record del risultato.  
  
 Se si elimina l'ultimo record rimanente nella **Recordset** dell'oggetto, il cursore rimane in uno stato indeterminato. Il **BOF** e **EOF** le proprietà possono rimanere **False** fino a quando non si prova a modificare la posizione del record corrente, a seconda del provider. Per altre informazioni, vedere [eliminazione record usando il metodo Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
