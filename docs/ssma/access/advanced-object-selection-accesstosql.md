---
title: Selezione avanzata di oggetti (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4d2b367f-8ac7-4534-b66f-10300ef64ebc
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a44e3882121347235141aacf879beea8127e3133
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62759747"
---
# <a name="advanced-object-selection--accesstosql"></a>Advanced Object Selection  (AccessToSQL)
Il **Advanced sezione oggetto** nella finestra di dialogo consente di filtrare gli oggetti di database usando le stringhe e le sottostringhe nel nome dell'oggetto e quindi selezionare o deselezionare gli oggetti. SSMA esegue operazioni di conversione e la migrazione per oggetti selezionati.  
  
Per accedere a questa finestra di dialogo, fare doppio clic in una finestra di esplorazione di metadati e quindi selezionare **Selezione oggetto avanzata**.  
  
Quando si apre la finestra di dialogo, fare clic su **Mostra gli elementi di sottocategorie** per visualizzare tutti gli oggetti con metadati caricato nel progetto. È quindi possibile immettere stringhe per filtrare gli elementi. Ad esempio, immettere la stringa "company" per visualizzare tutti gli elementi con nomi che includono tale stringa.  
  
Prima di usare questa finestra di dialogo, è possibile forzare SSMA per caricare tutti i metadati dal salvataggio del progetto o la conversione di schemi.  
  
## <a name="options"></a>Opzioni  
**Seleziona tutti gli elementi**  
Aggiunge un segno di spunta accanto a tutti gli elementi. Verranno selezionati immediatamente questi elementi nel Visualizzatore metadati.  
  
**Deseleziona tutti gli elementi**  
Rimuove il segno di spunta accanto a tutti gli elementi. Questi elementi verranno cancellati immediatamente nella finestra di esplorazione di metadati.  
  
**Modalità di visualizzazione elenco**  
Consente di visualizzare gli elementi in un elenco filtrati.  
  
**Modalità di visualizzazione tabella**  
Consente di visualizzare gli elementi in una tabella filtrati.  
  
**Caricare solo gli elementi visualizzati**  
Attiva o disattiva la visualizzazione delle categorie o elementi. Quando si seleziona questo pulsante, SSMA Mostra tutti gli elementi che corrispondono ai criteri di filtro e quelli che sono stati caricati in precedenza. Quando questo pulsante non è selezionato, tramite SSMA vengono illustrate le cartelle di categoria.  
  
**Filter**  
Immettere la stringa da usare per filtrare gli elementi. Ad esempio, per trovare tutti disponibili elementi che contengono la stringa "ID" nel nome dell'elemento, immettere la stringa "ID" nel **filtro** casella.  
  
Se gli elementi corrispondono ai criteri di filtro, le categorie o elementi verranno visualizzato mentre si digita la stringa. Per visualizzare gli elementi corrispondenti, si consiglia di scegliere la **visualizzati solo gli elementi caricati** pulsante.  
  
**Cancella filtro**  
Cancella il **filtro** casella.  
  
