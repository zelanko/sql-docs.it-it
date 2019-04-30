---
title: Uso dei metodi AddNew nell'immediato e modalità Batch | Microsoft Docs
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
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6295e4499a6f6f25f9111497012f2e9f1d6dc421
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184939"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Uso di AddNew in modalità batch e immediata
Il comportamento dei **AddNew** metodo dipende dalla modalità di aggiornamento del **Recordset** oggetto e se si passa il *FieldList* e *valori*argomenti.  
  
 In modalità di aggiornamento immediato (in cui il provider scrive le modifiche all'origine dati sottostante non appena viene chiamato il **aggiornare** metodo), la chiamata il **AddNew** metodo senza argomenti imposta il  **Proprietà EditMode** proprietà **adEditAdd.** Il provider di memorizza nella cache qualsiasi valore di campo modificato in locale. Chiama il **Update** metodo invia il nuovo record nel database e reimposta il **EditMode** proprietà **adEditNone.** Se si passa il *FieldList* e *valori* argomenti, ADO genera immediatamente il nuovo record nel database (nessun **Update** è necessario chiamare); il **EditMode**  non modifica il valore di proprietà (**adEditNone**).  
  
 In modalità di aggiornamento batch, chiama il **AddNew** metodo senza argomenti imposta il **EditMode** proprietà **adEditAdd**. Il provider di memorizza nella cache qualsiasi valore di campo modificato in locale. Chiama il **Update** metodo aggiunge il nuovo record corrente **Recordset** e reimposta il **EditMode** proprietà **adEditNone**, ma il provider invia le modifiche al database sottostante fino a quando non si chiama il **UpdateBatch** (metodo). Se si passa il *FieldList* e *valori* argomenti, ADO invia il nuovo record per il provider per l'archiviazione in una cache, è necessario chiamare il **UpdateBatch** per registrare il nuovo metodo registrare il database sottostante. Per altre informazioni sulle **Update** e **UpdateBatch**, vedere [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).
