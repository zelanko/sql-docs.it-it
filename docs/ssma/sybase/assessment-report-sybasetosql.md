---
title: Report di valutazione (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aae49bb6eb8ecf067911b2cb64017af0f3143aa0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63132794"
---
# <a name="assessment-report-sybasetosql"></a>Report di valutazione (SybaseToSQL)
La finestra di Report di valutazione Mostra i risultati della conversione di oggetti di database da [!INCLUDE[tsql](../../includes/tsql-md.md)] informazioni sulla sintassi, e può inoltre la Guida è stimare la complessità e i costi dei progetti di migrazione.  
  
Per accedere al Report di valutazione, selezionare gli oggetti da convertire in Visualizzatore metadati di origine, fare doppio clic su **database**, quindi selezionare **crea Report**.  
  
## <a name="options"></a>Opzioni  
**Statistiche di conversione**  
Mostra le statistiche di conversione dal tipo di istruzione. Questo riquadro è visibile solo quando un oggetto di gruppo, ad esempio uno schema, o nel riquadro di sinistra è selezionato un oggetto senza codice.  
  
**Oggetti in base alla categoria**  
Mostra le statistiche di conversione dal tipo di oggetto. Questo riquadro è visibile solo quando un oggetto di gruppo, ad esempio uno schema, o nel riquadro di sinistra è selezionato un oggetto senza codice.  
  
**Statistiche**  
Mostra le statistiche di conversione per l'oggetto selezionato. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro. Potrebbe essere necessario espandere **statistiche** per visualizzare questo riquadro.  
  
**Navigazione di origine**  
Visualizzare il codice di ambiente del servizio App per l'oggetto selezionato ed evidenzia il codice che non è stato convertito in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro.  
  
Fare clic sui numeri di riga per selezionare o deselezionare i segnalibri. Usare i pulsanti nella parte superiore del riquadro per esplorare il codice.  
  
**Navigazione di destinazione**  
Mostra la conversione del risultante [!INCLUDE[tsql](../../includes/tsql-md.md)] codice per l'oggetto selezionato e i messaggi di errore per il codice che non è stato convertito. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro.  
  
Fare clic sui numeri di riga per selezionare o deselezionare i segnalibri. Usare i pulsanti nella parte superiore del riquadro per esplorare il codice.  
  
**Riquadro messaggi**  
Viene illustrato l'errori, avvisi e messaggi di informazioni che vengono generati quando si crea il report di valutazione. I messaggi vengono raggruppati per numero. Per visualizzare il codice che ha causato l'errore, fare clic su **errore**, **avviso**, o **Info**, espandere la categoria dei messaggi e quindi fare clic su un messaggio.  
  
