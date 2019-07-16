---
title: Raccolta di campi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 197a57b8a9b9ea2927a057733992a02c731a335a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923930"
---
# <a name="the-fields-collection"></a>Raccolta Fields
Il **campi** insieme è uno degli insiemi intrinseci di ADO. Una raccolta è un set ordinato di elementi che può essere indicato come un'unità. Per altre informazioni sulle raccolte di ADO, vedere [il modello a oggetti ADO](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 Il **i campi** raccolta contiene un **campo** dell'oggetto per ogni campo (colonna) nei **Recordset**. Come tutte le raccolte di ADO, ha **conteggio** e **elemento** le proprietà, nonché **Append** e **Aggiorna** metodi. Include inoltre **CancelUpdate**, **eliminare**, **Risincronizza**, e **Update** metodi, che non sono disponibili ad altre raccolte di ADO.  
  
## <a name="examining-the-fields-collection"></a>Esaminare la raccolta di campi  
 Prendere in considerazione la **i campi** raccolta del campione **Recordset** introdotte in questa sezione. L'esempio **Recordset** è stata derivata dall'istruzione SQL  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 In questo modo, si rileverà che il **Recordset Fields** insieme contiene tre campi.  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 Questo codice determina semplicemente il numero di **campo** gli oggetti nel **campi** insieme utilizzando il **conteggio** proprietà e scorre in ciclo l'insieme restituendo il valore di il **Name** proprietà per ogni **campo** oggetto. È possibile usare molte altre **campo** proprietà per ottenere informazioni su un campo. Per altre informazioni sull'esecuzione di query su un **campo**, vedere [il campo oggetto](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Conteggio delle colonne  
 Come è prevedibile, il **conteggio** proprietà restituisce il numero effettivo di **campo** gli oggetti nel **campi** raccolta. Poiché per i membri di una raccolta di numerazione inizia da zero, è consigliabile codificare sempre i cicli a partire dal membro zero e terminando con il valore della **conteggio** proprietà meno 1. Se si utilizza Microsoft Visual Basic e si desidera eseguire un ciclo attraverso i membri di una raccolta senza il controllo il **conteggio** proprietà, utilizzare il **For Each... Avanti** comando.  
  
 Se il **conteggio** proprietà è zero, non sono presenti oggetti nella raccolta.  
  
## <a name="getting-to-the-field"></a>Introduzione al campo  
 Come con qualsiasi raccolta di ADO, il **elemento** proprietà la proprietà predefinita della raccolta. Restituisce i singoli **campo** oggetto specificato dal nome o indice passato ad esso. Di conseguenza, le istruzioni seguenti sono equivalenti per il campione **Recordset**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 Se questi metodi sono equivalenti, cui è preferibile? Dipende. Usando un indice per recuperare un **campo** dalla raccolta è più veloce perché accede il **campo** direttamente senza dover eseguire una ricerca di stringa. D'altra parte, l'ordine degli **campi** all'interno della raccolta deve essere nota, e se l'ordine viene modificato, il riferimento al **del campo** indice dovrà essere modificato ovunque si trovi. Anche se leggermente più lento, utilizzando il nome del **campo** è più flessibile perché non variano in base all'ordine dei **campi** nella raccolta.  
  
## <a name="using-the-refresh-method"></a>Usando il metodo di aggiornamento  
 A differenza di alcune altre raccolte di ADO, usando il **Refresh** metodo sul **campi** raccolta non ha alcun effetto visibile. Per recuperare le modifiche apportate dalla struttura di database sottostante, è necessario usare il **Requery** metodo, o se il **Recordset** objekt nepodporuje segnalibri, il **MoveFirst**metodo, che causerà il comando da eseguire confrontandolo con il provider di nuovo.  
  
## <a name="adding-fields-to-a-recordset"></a>Aggiunta di campi a un set di record  
 Il **Append** metodo viene utilizzato per aggiungere campi a un **Recordset**.  
  
 È possibile usare la **Append** metodo per creare un **Recordset** a livello di codice senza dover aprire una connessione a un'origine dati. Se si verificherà un errore di run-time di **Append** metodo viene chiamato sul **campi** raccolta di un elemento aperto **Recordset** o in un **Recordset** in cui il **ActiveConnection** proprietà è stata impostata. È possibile aggiungere campi solo a un **Recordset** che non è aperta e non è ancora stato connesso a un'origine dati. Tuttavia, per specificare i valori per l'oggetto appena aggiunto **i campi**, il **Recordset** deve innanzitutto essere aperto.  
  
 Gli sviluppatori devono spesso una posizione per archiviare alcuni dati temporaneamente o alcuni dei dati su cui agire come se provenissero da un server in modo da partecipare nel data binding in un'interfaccia utente. ADO (in combinazione con il [Microsoft Cursor Service per OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) consente agli sviluppatori di compilare un oggetto vuoto **Recordset** oggetto che specifica le informazioni di colonna e chiamando **aprire**. Nell'esempio seguente, vengono aggiunti tre nuovi campi a una nuova **Recordset** oggetto. Il **Recordset** viene aperto, due nuovi record vengono aggiunti e il **Recordset** è persistente in un file. (Per altre informazioni sulle **Recordset** persistenza, vedere [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 L'utilizzo del **accodare i campi** metodo differisce tra le **Recordset** oggetto e il **Record** oggetto. Per altre informazioni sul **Record** oggetti, vedere [record e flussi](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di recordset gerarchici](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
