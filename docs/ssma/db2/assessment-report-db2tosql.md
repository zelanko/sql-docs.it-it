---
title: Report di valutazione (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6981a3ae7808f727ed3a2d246f21f3159bbeac6e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299006"
---
# <a name="assessment-report-db2tosql"></a>Report di valutazione (DB2ToSQL)
La finestra di Report di valutazione Mostra i risultati della conversione di oggetti di database da [!INCLUDE[tsql](../../includes/tsql-md.md)] informazioni sulla sintassi, e può inoltre la Guida è stimare la complessità e i costi dei progetti di migrazione.  
  
Per accedere al Report di valutazione, selezionare gli oggetti da convertire in Visualizzatore metadati di origine, fare doppio clic su **schemi** oppure **sinonimi**, quindi selezionare **crea Report**.  
  
## <a name="options"></a>Opzioni  
  
|||  
|-|-|  
|Nome|Definizione|  
|**Statistiche di conversione**|Mostra le statistiche di conversione dal tipo di istruzione. Questo riquadro è visualizzato quando un oggetto di gruppo, ad esempio uno schema, o nel riquadro di sinistra è selezionato un oggetto senza codice.|  
|**Oggetti per categorie**|Mostra il numero di oggetti in base alla categoria. Questo riquadro è visibile solo quando un oggetto di gruppo, ad esempio uno schema, o nel riquadro di sinistra è selezionato un oggetto senza codice.|  
|**Statistiche**|Mostra le statistiche di conversione per l'oggetto selezionato. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro. Potrebbe essere necessario espandere **statistiche**, che viene immediatamente sopra il **origine** riquadro per visualizzare questo riquadro.|  
|**Origine**|Visualizzare il codice di DB2 per l'oggetto selezionato ed evidenzia il codice che non è stato convertito in [!INCLUDE[tsql](../../includes/tsql-md.md)]. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro.<br /><br />Fare clic sui numeri di riga per selezionare o deselezionare i segnalibri. Usare i pulsanti nella parte superiore del riquadro per esplorare il codice.|  
|**Destinazione**|Mostra la conversione del risultante [!INCLUDE[tsql](../../includes/tsql-md.md)] codice per l'oggetto selezionato e i messaggi di errore per il codice che non è stato convertito. Questo riquadro è visibile solo quando è selezionato un oggetto singoli con il codice nel riquadro sinistro.<br /><br />Fare clic sui numeri di riga per selezionare o deselezionare i segnalibri. Usare i pulsanti nella parte superiore del riquadro per esplorare il codice.|  
|**Riquadro messaggi**|Viene illustrato l'errori, avvisi e messaggi informativi che sono stati generati durante la creazione di report di valutazione. I messaggi vengono raggruppati per numero. Per visualizzare il codice che ha causato l'errore, fare clic su **errori**, **avvisi**, o **Info**, espandere la categoria dei messaggi e quindi fare clic su un messaggio.|  
  
