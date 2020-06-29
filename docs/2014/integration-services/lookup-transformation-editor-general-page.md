---
title: Editor trasformazione Ricerca (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1798e5a65c27e10de7da608b391d8df3f6e7d03
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440218"
---
# <a name="lookup-transformation-editor-general-page"></a>Editor trasformazione Ricerca (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo Editor trasformazione Ricerca per selezionare la modalità di cache, selezionare il tipo di connessione e specificare la modalità di gestione delle righe senza voci corrispondenti.  
  
 Per ulteriori informazioni sulla trasformazione Ricerca, vedere [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Full Cache**  
 Generare e caricare il set di dati di riferimento nella cache prima dell'esecuzione della trasformazione Ricerca.  
  
 **Partial Cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Caricare le righe con le voci corrispondenti nel set di dati di riferimento e le righe senza voci corrispondenti nel set di dati nella cache.  
  
 **Nessuna cache**  
 Generare il set di dati di riferimento durante l'esecuzione della trasformazione Ricerca. Non sono stati caricati dati in cache.  
  
 **Gestione connessione della cache**  
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
 [Gestione connessione della cache](connection-manager/cache-connection-manager.md)   
 [Editor trasformazione Ricerca &#40;pagina connessione&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor trasformazione Ricerca &#40;pagina colonne&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca &#40;pagina avanzate&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
