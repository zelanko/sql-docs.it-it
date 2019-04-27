---
title: Procedura di modifica delle proprietà dell'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96604a09811626a304502dc05ef4f7e9edcd0359
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771229"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>Procedura di modifica delle proprietà dell'istanza di CDC
  In questa procedura viene illustrato come utilizzare CDC Designer Console per modificare le proprietà di configurazione per un'istanza di CDC.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>Per modificare le proprietà di configurazione di un'istanza di CDC.  
  
1.  Scegliere **CDC Designer Console** dal menu **Start**.  
  
2.  Nel riquadro sinistro espandere **Change Data Capture** , quindi espandere il servizio che contiene l'istanza con le proprietà che si desidera modificare.  
  
3.  Selezionare il nome dell'istanza in cui si desidera modificare le proprietà.  
  
4.  Nel riquadro Actions sul lato destro di CDC Designer Console, fare clic su **Properties**.  
  
     È inoltre possibile fare clic con il pulsante destro del mouse sull'istanza in cui si desidera modificare le proprietà e selezionare **Proprietà**.  
  
5.  Nell'editor delle proprietà modificare le proprietà nelle schede seguenti:  
  
    -   **Oracle**: Usare la scheda **Oracle** nell'editor delle proprietà per modificare la descrizione fornita nella pagina Create CDC database (Crea database CDC) della New Instance Wizard (Creazione guidata nuova istanza) e le informazioni di connessione al database di log mining Oracle.  
  
         Per informazioni sul contenuto di questa scheda che è possibile modificare, vedere [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
    -   **Tabelle**: Utilizzare la scheda **Tabelle** per apportare modifiche alle tabelle e alle colonne selezionate dal database di origine Oracle.  
  
         Per informazioni sul contenuto di questa scheda che è possibile modificare, vedere [Edit Tables](edit-tables.md).  
  
    -   **Script**: usare la scheda **Script** per eseguire o rieseguire uno script nel database di origine Oracle per la configurazione della registrazione supplementare.  
  
         Per informazioni sulle operazioni possibili in questa scheda, vedere [Review and Generate Supplemental Logging Scripts](review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Avanzate**: Utilizzare la scheda **Avanzate** per aggiungere proprietà speciali all'istanza di CDC.  
  
         Per informazioni sulle operazioni possibili in questa scheda, vedere [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
  
