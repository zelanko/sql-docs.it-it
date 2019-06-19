---
title: L'eliminazione di record usando il metodo Delete | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b4798e2658bf23edaf7cd04fb819e26de2a55cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700826"
---
# <a name="deleting-records-using-the-delete-method"></a>Eliminazione di record con il metodo Delete
Usando il **eliminare** metodo contrassegna il record corrente o un gruppo di record in un **Recordset** oggetto per l'eliminazione. Se il **Recordset** oggetto non consente l'eliminazione di record, si verifica un errore. Se si è in modalità di aggiornamento immediato, le eliminazioni verranno eseguite immediatamente nel database. Se non è possibile eliminare un record (a causa di violazioni di integrità del database, ad esempio), il record rimarranno nella modalità di modifica dopo la chiamata a **Update.** Ciò significa che è necessario annullare l'aggiornamento con [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) prima di uscire il record corrente (ad esempio, usando [Close](../../../ado/reference/ado-api/close-method-ado.md), [spostare](../../../ado/reference/ado-api/move-method-ado.md), o [ NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)).  
  
 Se si è in modalità di aggiornamento batch, i record contrassegnati per l'eliminazione dalla cache e l'eliminazione effettiva si verifica quando si chiama il **UpdateBatch** (metodo). (Per visualizzare i record eliminati, impostare il **filtro** proprietà **adFilterAffectedRecords** dopo **Elimina** viene chiamato.)  
  
 Tentativo di recuperare i valori dei campi del record eliminato genera un errore. Dopo aver eliminato il record corrente, il record eliminato rimane invariato fino a quando non si sposta in un altro record. Una volta si allontanano del record eliminato, non è più accessibile.  
  
 Se le eliminazioni in una transazione vengono nidificate, è possibile ripristinare i record eliminati con il **RollbackTrans** (metodo). Se si è in modalità di aggiornamento batch, è possibile annullare l'eliminazione in sospeso o un gruppo di eliminazioni in sospeso utilizzando il **CancelBatch** (metodo).  
  
 Se il tentativo di eliminare i record non riesce a causa di un conflitto con i dati sottostanti (ad esempio, un record è già stato eliminato da un altro utente), il provider restituisce avvisi per i **errori** raccolta ma non arrestano programma esecuzione. Errore di run-time si verifica solo se sono presenti conflitti in tutti i record richiesti.  
  
 Se il **tabella univoca** dinamica viene impostata e il **Recordset** è il risultato dell'esecuzione di un'operazione di JOIN in più tabelle, il **Elimina** metodo elimina solo righe dalla tabella menzionata nel **Unique Table** proprietà.  
  
 Il **eliminare** metodo accetta un argomento facoltativo che consente di specificare quali record sono coinvolti i **eliminare** operazione. Gli unici valori validi per questo argomento sono uno dei seguente ADO **AffectEnum** costanti enumerate:  
  
-   **adAffectCurrent** interessa solo il record corrente.  
  
-   **adAffectGroup** interessa solo i record che soddisfano corrente **filtro** l'impostazione della proprietà. Il **filtro** proprietà deve essere impostata su un **FilterGroupEnum** valore o una matrice di **segnalibri** per usare questa opzione.  
  
 Il codice seguente illustra un esempio di definizione **adAffectGroup** quando si chiama il **eliminare** (metodo). Questo esempio vengono aggiunti alcuni record al campione **Recordset** e aggiorna il database. Quindi Filtra i **Recordset** usando la **adFilterAffectedRecords** costante enumerata di filtro, che rende visibili in solo il record appena aggiunto il **Recordset.** Infine, chiama il **eliminare** metodo e specifica che tutti i record che soddisfano corrente **filtro** deve essere eliminata l'impostazione della proprietà (i nuovi record).  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
