---
title: Aggiunta di record tramite AddNew | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: abdd3bf7e23c74624a7eaa70c102112593fd3648
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761407"
---
# <a name="adding-records-using-addnew-method"></a>Aggiunta di record tramite il metodo AddNew
Si tratta della sintassi di base del metodo **AddNew** :

 *Recordset*. *TextField*(AddNew), *valori*

 Gli argomenti *FieldName* e *values* sono facoltativi. *FieldName* è un singolo nome o una matrice di nomi o posizioni ordinali dei campi nel nuovo record.

 L'argomento *values* può essere un singolo valore o una matrice di valori per i campi nel nuovo record.

 In genere, quando si intende aggiungere un singolo record, si chiamerà il metodo **AddNew** senza argomenti. In particolare, si chiamerà **AddNew**; impostare il **valore** di ogni campo nel nuovo record; quindi chiamare **Update** o **UpdateBatch**o entrambi. È possibile assicurarsi che il **Recordset** supporti l'aggiunta di nuovi record utilizzando la proprietà **Supports** con la costante enumerata **adAddNew** .

 Il codice seguente usa questa tecnica per aggiungere un nuovo spedizioniere al **Recordset**di esempio. SQL Server fornisce automaticamente il valore del campo IDCorriere. Il codice non tenta pertanto di fornire un valore di campo per i nuovi record.

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

## <a name="remarks"></a>Osservazioni
 Poiché questo codice utilizza un **Recordset** disconnesso con un cursore sul lato client in modalità batch, è necessario riconnettere il **Recordset** all'origine dati con un nuovo oggetto **connessione** prima di poter chiamare il metodo **UpdateBatch** per inviare le modifiche al database. Questa operazione viene eseguita facilmente usando la nuova funzione **GetNewConnection**.
