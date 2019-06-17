---
title: Gestire modifiche a viste origine dati e origini dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac551a708433e973ada499f0e7504bc75516e756
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074772"
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>Gestire modifiche a viste origine dati e origini dati
  Quando si riesegue la Generazione guidata schema, vengono riutilizzate la stessa origine dei dati e la stessa vista origine dati utilizzate durante la generazione originale. Se si aggiunge un'origine dei dati oppure una vista origine dati, il nuovo elemento verrà ignorato dalla procedura guidata. Se si elimina l'origine dei dati o la vista origine dati originale dopo la generazione iniziale, sarà necessario eseguire la procedura guidata dall'inizio. Verranno inoltre eliminate tutte le impostazioni precedenti della procedura guidata. Tutti gli oggetti esistenti in un database sottostante associati a un'origine dei dati o una vista origine dati eliminata verranno considerati come oggetti creati dall'utente durante la successiva esecuzione della Generazione guidata schema.  
  
 Se la vista origine dati non riflette lo stato effettivo del database sottostante al momento della generazione, è possibile che nella Generazione guidata schema vengano rilevati errori durante la generazione dello schema del database dell'area di interesse. Se il tipo di dati specificato per una colonna nella vista origine dati è **int**ma il tipo di dati effettivo della colonna è **string**, ad esempio, il tipo di dati per la chiave esterna verrà impostato nella Generazione guidata schema su **INT** in conformità con la vista origine dati e si verificherà quindi un errore durante la creazione della relazione poiché il tipo effettivo è **string**.  
  
 Se invece si modifica la stringa di connessione dell'origine dei dati impostando un database diverso rispetto alla generazione precedente, non verrà generato alcun errore. Verrà utilizzato il nuovo database senza alcuna modifica al database precedente.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla generazione incrementale](understanding-incremental-generation.md)  
  
  
