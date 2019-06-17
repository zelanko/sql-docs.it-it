---
title: Aggiunta di record | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 87d8358344d75cd6995d43d081abbec7aeaabe1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701054"
---
# <a name="adding-records-to-a-recordset"></a>Aggiunta di record a un set di record
Usare la **AddNew** metodo per creare e inizializzare un nuovo record in un oggetto esistente **Recordset**. È possibile usare la **supporta** metodo con un **CursorOptionEnum** pari a **adAddNew** per verificare se è possibile aggiungere record corrente **Recordset** oggetti.

 Dopo aver chiamato il **AddNew** metodo, il nuovo record del record corrente e rimane tale dopo la chiamata il **Update** (metodo). Se il **Recordset** objekt nepodporuje segnalibri, potrebbe non essere in grado di accedere al record di nuovo dopo il passaggio a un altro record. Pertanto, a seconda del tipo di cursore, potrebbe essere necessario chiamare il **Requery** metodo per rendere accessibile il nuovo record.

 Se si chiama **AddNew** durante la modifica del record corrente o durante l'aggiunta di un nuovo record, chiama il metodo ADO le **Update** metodo per salvare eventuali modifiche e quindi crea il nuovo record.

 In questa sezione vengono trattati gli argomenti seguenti.

-   [Aggiunta di record mediante AddNew](../../../ado/guide/data/adding-records-using-addnew.md)

-   [Aggiunta di più campi](../../../ado/guide/data/adding-multiple-fields.md)

-   [Determinazione della modalità di modifica](../../../ado/guide/data/determining-edit-mode.md)

-   [Uso di AddNew in modalità batch e immediata](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)
