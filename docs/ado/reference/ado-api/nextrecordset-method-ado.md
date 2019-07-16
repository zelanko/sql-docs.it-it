---
title: Esempio di metodo NextRecordset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c7af4f5d217670ab23e71a3c53ccd5cf7944b0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932030"
---
# <a name="nextrecordset-method-ado"></a>Metodo NextRecordset (ADO)
Cancella l'oggetto corrente [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dell'oggetto e restituisce il successivo **Recordset** anticipando attraverso una serie di comandi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Recordset** oggetto. Nel modello di sintassi *recordset1* e *recordset2* può essere lo stesso **Recordset** oggetto oppure è possibile usare oggetti separati. Quando si usa separato **Recordset** oggetti, reimpostare il **ActiveConnection** proprietà sull'oggetto originale **Recordset** (*recordset1*) Dopo aver **NextRecordset** è stato chiamato verrà generato un errore.  
  
#### <a name="parameters"></a>Parametri  
 *RecordsAffected*  
 facoltativo. Oggetto **lungo** variabile in cui il provider restituisce il numero di record interessati dall'operazione corrente.  
  
> [!NOTE]
>  Questo parametro restituisce solo il numero di record interessati dall'operazione; non viene restituito un conteggio di record da un'istruzione select usata per generare il **Recordset**.  
  
## <a name="remarks"></a>Note  
 Usare la **NextRecordset** metodo per restituire i risultati del comando successivo in un'istruzione composta comando o di una stored procedure che restituisce più risultati. Se si apre un **Recordset** oggetto basato su un'istruzione composta comando (ad esempio, "selezionare \* FROM table1; Selezionare \* da table2 ") usando il [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) metodo su un [comando](../../../ado/reference/ado-api/command-object-ado.md) o il [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo su una **Recordset**, ADO esegue solo il primo comando e restituisce i risultati in *recordset*. Per accedere ai risultati dei comandi successivi nell'istruzione, chiama il **NextRecordset** (metodo).  
  
 Finché sono presenti altri risultati e il **Recordset** che contiene le istruzioni composte non è disconnesso o sottoposta a marshalling oltre i limiti dei processi, il **NextRecordset** metodo continueranno a restituire **Recordset** oggetti. Se un comando che restituiscono righe viene eseguito correttamente, ma non restituisce alcun record, l'oggetto restituito **Recordset** oggetto sarà aperto ma vuoto. Test per questo caso, verificando che il [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) e [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) le proprietà sono entrambi **True**. Se un comando non restituiscono righe viene eseguito correttamente, l'oggetto restituito **Recordset** oggetto verrà chiusa, è possibile verificare controllando il [stato](../../../ado/reference/ado-api/state-property-ado.md) proprietà il **Recordset**. Quando non sono presenti altri risultati, *recordset* verrà impostato su *Nothing*.  
  
 Il **NextRecordset** metodo non è disponibile in un disconnesso **Recordset** oggetto, in cui [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) è stata impostata su **Nothing**(in Microsoft Visual Basic) o NULL (in altre lingue).  
  
 Se una modifica è in corso in modalità di aggiornamento immediato, chiamando il **NextRecordset** metodo genera un errore, chiamare il [aggiornare](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo prima.  
  
 Passare i parametri per più di un comando nell'istruzione composta compilando i [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) insieme, o passando una matrice con l'originale **Open** o **Execute** chiamata, i parametri devono essere nello stesso ordine nell'insieme o matrice, dei rispettivi comandi nella serie di comandi. È necessario completare la lettura di tutti i risultati prima di leggere i valori dei parametri output.  
  
 Il provider OLE DB determina quando viene eseguito ogni comando in un'istruzione composta. Il [Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), ad esempio, esegue tutti i comandi in un batch dopo aver ricevuto l'istruzione composta. L'oggetto risultante **recordset** vengono semplicemente restituite quando viene chiamato **NextRecordset**.  
  
 Tuttavia, altri provider di servizi potrebbe eseguire il comando successivo in un'istruzione solo dopo la chiamata di NextRecordset. Per questi provider, se si chiude in modo esplicito il **Recordset** object prima avanzando istruzione per istruzione del comando intero, ADO non vengono mai eseguiti i comandi rimanenti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo NextRecordset (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [Esempio di metodo NextRecordset (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
