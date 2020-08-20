---
description: Report di valutazione (AccessToSQL)
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5f1058947591fdd454ce181b2d098f88b183cbe1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497827"
---
# <a name="assessment-report-accesstosql"></a>Report di valutazione (AccessToSQL)
La finestra report di valutazione Mostra i risultati della conversione degli oggetti di database nella [!INCLUDE[tsql](../../includes/tsql-md.md)] sintassi e consente inoltre di stimare la complessità e il costo dei progetti di migrazione.  
  
Per creare un report di valutazione, selezionare gli oggetti da convertire in Esplora metadati di origine, fare clic con il pulsante destro del mouse su **database**e quindi scegliere **Crea report**. È inoltre possibile visualizzare questo report automaticamente dopo la conversione degli schemi. Il nome del report sarà tuttavia un report di conversione. Per ulteriori informazioni, vedere [Impostazioni progetto (GUI) (SSMA Common)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opzioni  
**Riquadro di esplorazione**  
Contiene una gerarchia di oggetti nel report di valutazione. Espandere cartelle per visualizzare singoli oggetti e sottocomponenti. Quando si fa clic su una categoria o un oggetto, nel riquadro dei dettagli vengono visualizzate le statistiche relative alla conversione per tale categoria o oggetto.  
  
**Riquadro dei dettagli**  
Mostra le statistiche di conversione o i messaggi di errore e di avviso per l'oggetto selezionato. Se, ad esempio, è selezionata la cartella tabelle, nel riquadro dei dettagli verrà visualizzato il numero di chiavi esterne, indici, chiavi primarie e tabelle convertite.  
  
**riquadro Messaggi**  
Mostra gli errori, gli avvisi e i messaggi informativi generati al momento della creazione del report di valutazione. I messaggi sono raggruppati per numero.  
  
Per visualizzare i dettagli del messaggio, fare clic su **errori**, **avvisi**o **messaggi**, quindi espandere un messaggio. SSMA visualizzerà l'elenco di oggetti con questo errore. Fare clic su un oggetto per visualizzare tutti i dettagli di conversione per l'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
[Guida di riferimento all'interfaccia utente (accesso)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
