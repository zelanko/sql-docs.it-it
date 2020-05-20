---
title: Uso di AddNew in modalità immediate e batch | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 93fc9cb388440a8efd9099d6ae82b110cb60b2d0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763072"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Uso di AddNew in modalità batch e immediata
Il comportamento del metodo **AddNew** dipende dalla modalità di aggiornamento dell'oggetto **Recordset** e dal fatto che vengano passati gli argomenti *FieldName* e *values* .  
  
 In modalità di aggiornamento immediato, in cui il provider scrive le modifiche nell'origine dati sottostante una volta chiamato il metodo **Update** , la chiamata al metodo **AddNew** senza argomenti imposta la proprietà **EditMode** su **adEditAdd.** Il provider memorizza nella cache le modifiche del valore del campo in locale. Se si chiama il metodo di **aggiornamento** , il nuovo record viene inserito nel database e viene reimpostata la proprietà **EditMode** su **adEditNone.** Se si passano gli argomenti *FieldName* e *values* , ADO inserisce immediatamente il nuovo record nel database (non è necessaria alcuna chiamata di **aggiornamento** ); il valore della proprietà **EditMode** non cambia (**adEditNone**).  
  
 In modalità di aggiornamento batch, la chiamata al metodo **AddNew** senza argomenti imposta la proprietà **EditMode** su **adEditAdd**. Il provider memorizza nella cache le modifiche del valore del campo in locale. La chiamata al metodo **Update** aggiunge il nuovo record al **Recordset** corrente e reimposta la proprietà **EditMode** su **adEditNone**, ma il provider non invia le modifiche al database sottostante fino a quando non viene chiamato il metodo **UpdateBatch** . Se si passano gli argomenti *FieldName* e *values* , ADO invia il nuovo record al provider per l'archiviazione in una cache. è necessario chiamare il metodo **UpdateBatch** per inserire il nuovo record nel database sottostante. Per ulteriori informazioni su **Update** e **UpdateBatch**, vedere [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).
