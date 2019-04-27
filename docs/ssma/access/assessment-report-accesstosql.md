---
title: Report di valutazione (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1278552f1bfe1ccfb7ab250f843e86c62e63440b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62651081"
---
# <a name="assessment-report-accesstosql"></a>Assessment Report (AccessToSQL)
La finestra di Report di valutazione Mostra i risultati della conversione di oggetti di database da [!INCLUDE[tsql](../../includes/tsql-md.md)] informazioni sulla sintassi, e può inoltre la Guida è stimare la complessità e i costi dei progetti di migrazione.  
  
Per creare un report di valutazione, selezionare gli oggetti da convertire in metadati Esplora codice sorgente, fare doppio clic su **database**, quindi selezionare **crea Report**. È anche possibile visualizzare questo rapporto automaticamente dopo la conversione di schemi. Tuttavia, il nome del report sarà Report di conversione. Per altre informazioni, vedere [Project. le impostazioni (GUI) (SSMA comuni)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opzioni  
**Riquadro di esplorazione**  
Contiene una gerarchia di oggetti nel report di valutazione. Espandere le cartelle per visualizzare i sottocomponenti e singoli oggetti. Quando si fa clic su una categoria o un oggetto, le statistiche di conversione relative alla categoria o oggetto visualizzate nel riquadro dei dettagli.  
  
**Riquadro dei dettagli**  
Mostra la conversione dei messaggi di avviso o di statistiche e di errore per l'oggetto selezionato. Ad esempio, se si seleziona la cartella di tabelle, riquadro dei dettagli mostrerà il numero di chiavi esterne, indici, chiavi primarie e le tabelle che sono state convertite.  
  
**Riquadro messaggi**  
Viene illustrato l'errori, avvisi e messaggi informativi che sono stati generati quando è stato creato il report di valutazione. I messaggi vengono raggruppati per numero.  
  
Per visualizzare i dettagli del messaggio, fare clic su **errori**, **avvisi**, o **messaggi**, quindi espandere un messaggio. SSMA verrà visualizzato l'elenco di oggetti che hanno questo errore. Fare clic su un oggetto per visualizzare tutte le informazioni dettagliate sulla conversione per l'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
[Reference(Access) dell'interfaccia utente](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
