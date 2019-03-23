---
title: Editor trasformazione ricerca (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4aa5b08a35a2eaf0d82b79145ecacde9d50579ee
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374169"
---
# <a name="lookup-transformation-editor-general-page"></a>Editor trasformazione Ricerca (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo Editor trasformazione Ricerca per selezionare la modalità di cache, selezionare il tipo di connessione e specificare la modalità di gestione delle righe senza voci corrispondenti.  
  
 Per ulteriori informazioni sulla trasformazione Ricerca, vedere [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Full Cache**  
 Generare e caricare il set di dati di riferimento nella cache prima dell'esecuzione della trasformazione Ricerca.  
  
 **Partial Cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Caricare le righe con le voci corrispondenti nel set di dati di riferimento e le righe senza voci corrispondenti nel set di dati nella cache.  
  
 **No Cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Non sono stati caricati dati in cache.  
  
 **gestione connessione della cache**  
 Configurare la trasformazione Ricerca per l'utilizzo della gestione connessione della cache. L'opzione è disponibile solo se è stata selezionata anche l'opzione Full Cache.  
  
 **Gestione connessione OLE DB**  
 Configurare la trasformazione Ricerca per l'utilizzo della gestione connessione OLE DB.  
  
 **Specificare come gestire le righe senza voci corrispondenti**  
 Selezionare un'opzione per la gestione delle righe che non dispongono di almeno una voce corrispondente nel set di dati di riferimento.  
  
 Quando si seleziona **Reindirizza righe all'output nessuna corrispondenza**, le righe vengono reindirizzate a un output senza corrispondenze e non vengono gestite come errori. L'opzione **Errore** nella pagina **Output errori** della finestra di dialogo **Editor trasformazione Ricerca** non è disponibile.  
  
 Quando si seleziona un'altra opzione nella casella di riepilogo **Specificare come gestire le righe senza voci corrispondenti** , le righe vengono gestite come errori. L'opzione **Errore** nella pagina **Output errori** è disponibile.  
  
## <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://go.microsoft.com/fwlink/?LinkId=219518) su blogs.msdn.com  
  
## <a name="see-also"></a>Vedere anche  
 [Cache Connection Manager](connection-manager/cache-connection-manager.md)   
 [Editor trasformazione Ricerca &#40;pagina Connessione&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Colonne&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Avanzate&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
