---
title: Aggiunta di record mediante AddNew | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926286"
---
# <a name="adding-records-using-addnew-method"></a>Aggiunta di record mediante AddNew (metodo)
Si tratta la sintassi di base del **AddNew** metodo:

 *recordset*. AddNew *FieldList*, *valori*

 Il *FieldList* e *valori* gli argomenti sono facoltativi. *Elenco campi* è un singolo nome o una matrice di nomi o le posizioni ordinali dei campi nel nuovo record.

 Il *valori* argomento è un singolo valore o una matrice di valori per i campi nel nuovo record.

 In genere, quando si prevede di aggiungere un singolo record, chiama il **AddNew** metodo senza alcun argomento. In particolare, si chiamerà **AddNew**; impostare il **valore** di ogni campo nel nuovo record; e quindi chiamare **Update** oppure **UpdateBatch**, o entrambi. È possibile assicurarsi che il **Recordset** supporta l'aggiunta di nuovi record tramite il **supporta** proprietà con il **adAddNew** costante enumerata.

 Il codice seguente usa questa tecnica per aggiungere un nuovo spedizioniere al campione **Recordset**. SQL Server fornisce il valore del campo ShipperID automaticamente. Pertanto, il codice non tenta di fornire un valore di campo per i nuovi record.

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>Note
 Poiché questo codice Usa un disconnessa **Recordset** con un cursore lato client in modalità batch, è necessario riconnettere le **Recordset** all'origine dati con un nuovo **connessione** oggetto prima di poter chiamare le **UpdateBatch** metodo per registrare le modifiche al database. Ciò avviene con facilità usando la nuova funzione **GetNewConnection**.
