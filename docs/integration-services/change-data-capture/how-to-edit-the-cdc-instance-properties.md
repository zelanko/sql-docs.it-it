---
description: Procedura di modifica delle proprietà dell'istanza di CDC
title: Procedura di modifica delle proprietà dell'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2861b40dbe132e7c95b52802bd10ccd46c20c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426093"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>Procedura di modifica delle proprietà dell'istanza di CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  In questa procedura viene illustrato come utilizzare CDC Designer Console per modificare le proprietà di configurazione per un'istanza di CDC.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>Per modificare le proprietà di configurazione di un'istanza di CDC.  
  
1.  Scegliere **CDC Designer Console** dal menu **Start**.  
  
2.  Nel riquadro sinistro espandere **Change Data Capture** , quindi espandere il servizio che contiene l'istanza con le proprietà che si desidera modificare.  
  
3.  Selezionare il nome dell'istanza in cui si desidera modificare le proprietà.  
  
4.  Nel riquadro Actions sul lato destro di CDC Designer Console, fare clic su **Properties**.  
  
     È inoltre possibile fare clic con il pulsante destro del mouse sull'istanza in cui si desidera modificare le proprietà e selezionare **Proprietà**.  
  
5.  Nell'editor delle proprietà modificare le proprietà nelle schede seguenti:  
  
    -   **Oracle**: utilizzare la scheda **Oracle** nell'editor delle proprietà per modificare la descrizione fornita nella pagina Create CDC database della New Instance Wizard e le informazioni di connessione al database di log mining Oracle.  
  
         Per informazioni sul contenuto di questa scheda che è possibile modificare, vedere [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
    -   **Tables**: utilizzare la scheda **Tables** per apportare modifiche alle tabelle e alle colonne selezionate dal database di origine Oracle.  
  
         Per informazioni sul contenuto di questa scheda che è possibile modificare, vedere [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
    -   **Script**: usare la scheda **Script** per eseguire o rieseguire uno script nel database di origine Oracle per la configurazione della registrazione supplementare.  
  
         Per informazioni sulle operazioni possibili in questa scheda, vedere [Review and Generate Supplemental Logging Scripts](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Advanced**: utilizzare la scheda **Advanced** per aggiungere proprietà speciali all'istanza di CDC.  
  
         Per informazioni sulle operazioni possibili in questa scheda, vedere [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
  
