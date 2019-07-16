---
title: Proprietà BOF, EOF proprietà (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4932d3349c2d4e2948ddd28d9df3a30424064dcb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920380"
---
# <a name="bof-eof-properties-ado"></a>Proprietà BOF ed EOF (ADO)
-   **Proprietà BOF** indica che la posizione del record corrente è precedente al primo record in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
-   **EOF** indica che la posizione del record corrente è successiva all'ultimo record in un **Recordset** oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Il **BOF** e **EOF** restituiscono **booleano** valori.  
  
## <a name="remarks"></a>Note  
 Usare la **BOF** e **EOF** le proprietà per determinare se un **Recordset** oggetto contiene record o se sono stati superati i limiti di un **Recordset**  dell'oggetto quando si sposta da un record a altro.  
  
 Il **BOF** restituisce proprietà **True** (-1) se la posizione del record corrente è precedente al primo record e **False** (0) se la posizione del record corrente è il o dopo il primo record.  
  
 Il **EOF** restituisce proprietà **True** se la posizione del record corrente è successiva all'ultimo record e **False** se la posizione del record corrente è il o prima dell'ultimo record.  
  
 Se il **BOF** oppure **EOF** proprietà è **True**, nessun record corrente.  
  
 Se si apre un **Recordset** oggetti che non contiene record, il **BOF** e **EOF** sono impostate su **True** (vedere il [ RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) proprietà per ulteriori informazioni su questo stato di un **Recordset**). Quando si apre un **Recordset** oggetto che contiene almeno un record, il primo record corrisponde al record corrente e il **BOF** e **EOF** sono proprietà **False** .  
  
 Se si elimina l'ultimo record rimanente nella **Recordset** oggetto, il **BOF** e **EOF** proprietà restino **False** finché non si tentativo di modificare la posizione del record corrente.  
  
 Questa tabella mostra che **spostare** metodi sono consentiti con diverse combinazioni delle **BOF** e **EOF** proprietà.  
  
||Metodi MoveFirst,<br /><br /> MoveLast|MovePrevious,<br /><br /> Spostare < 0|Spostare 0|MoveNext,<br /><br /> Sposta > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**Proprietà BOF**=**True**, **EOF**=**False**|Allowed|Errore|Errore|Allowed|  
|**Proprietà BOF**=**False**, **EOF**=**True**|Allowed|Allowed|Errore|Errore|  
|Entrambi **True**|Errore|Errore|Errore|Errore|  
|Entrambi **False**|Allowed|Allowed|Allowed|Allowed|  
  
 Consentendo un' **spostare** metodo non garantisce che il metodo individuerà correttamente un record; in realtà indica che la chiamata specificato **spostare** metodo non genererà un errore.  
  
 La tabella seguente mostra cosa accade ai **BOF** e **EOF** le impostazioni delle proprietà quando si chiama varie **spostare** metodi, ma non è possibile individuare correttamente il record.  
  
||PROPRIETÀ BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**, **MoveLast**|Impostare su **True**|Impostare su **True**|  
|**Spostare** 0|Nessuna modifica|Nessuna modifica|  
|**MovePrevious**, **spostare** < 0|Impostare su **True**|Nessuna modifica|  
|**MoveNext**, **spostare** > 0|Nessuna modifica|Impostare su **True**|  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà BOF, EOF e segnalibro (esempio di proprietà (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Proprietà BOF, EOF e segnalibro esempio di proprietà (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
