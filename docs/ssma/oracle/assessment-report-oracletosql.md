---
title: Report di valutazione (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 75fdb97b5b7d763694289d762edc65b4536a86c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264520"
---
# <a name="assessment-report-oracletosql"></a>Report di valutazione (OracleToSQL)
La finestra report di valutazione Mostra i risultati della conversione degli oggetti di database [!INCLUDE[tsql](../../includes/tsql-md.md)] nella sintassi e consente inoltre di stimare la complessità e il costo dei progetti di migrazione.  
  
Per accedere al report di valutazione, selezionare gli oggetti da convertire in Esplora metadati di origine, fare clic con il pulsante destro del mouse su **schemi** o **sinonimi**e quindi scegliere **Crea report**.  
  
## <a name="options"></a>Opzioni  
  
|||  
|-|-|  
|Termine|Definizione|  
|**Statistiche di conversione**|Mostra le statistiche di conversione per tipo di istruzione. Questo riquadro è visibile quando si seleziona un oggetto gruppo, ad esempio uno schema, o un oggetto senza codice nel riquadro sinistro.|  
|**Oggetti per categorie**|Mostra il numero di oggetti per categoria. Questo riquadro è visibile solo quando si seleziona un oggetto gruppo, ad esempio uno schema, o un oggetto senza codice nel riquadro sinistro.|  
|**Statistiche**|Mostra le statistiche di conversione per l'oggetto selezionato. Questo riquadro è visibile solo quando si seleziona un singolo oggetto con codice nel riquadro sinistro. Per visualizzare questo riquadro, potrebbe essere necessario espandere **Statistics**, che si trova immediatamente sopra il riquadro di **origine** .|  
|**origine**|Mostra il codice Oracle per l'oggetto selezionato ed evidenzia il codice che non è stato convertito [!INCLUDE[tsql](../../includes/tsql-md.md)]in. Questo riquadro è visibile solo quando si seleziona un singolo oggetto con codice nel riquadro sinistro.<br /><br />Per impostare o cancellare i segnalibri, fare clic sui numeri di riga. Utilizzare i pulsanti nella parte superiore del riquadro per spostarsi nel codice.|  
|**Destinazione**|Mostra il codice risultante [!INCLUDE[tsql](../../includes/tsql-md.md)] della conversione per l'oggetto selezionato e i messaggi di errore per il codice che non è stato convertito. Questo riquadro è visibile solo quando si seleziona un singolo oggetto con codice nel riquadro sinistro.<br /><br />Per impostare o cancellare i segnalibri, fare clic sui numeri di riga. Utilizzare i pulsanti nella parte superiore del riquadro per spostarsi nel codice.|  
|**riquadro Messaggi**|Mostra gli errori, gli avvisi e i messaggi informativi generati durante la creazione del report di valutazione. I messaggi sono raggruppati per numero. Per visualizzare il codice che ha causato l'errore, fare clic su **errori**, **avvisi**o **informazioni**, espandere la categoria di messaggi e quindi fare clic su un messaggio.|  
  
