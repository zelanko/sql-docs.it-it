---
title: Procedura di gestione di un'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd64fe5cad5f85c41830d25dce279ba09915626b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391529"
---
# <a name="how-to-manage-a-cdc-instance"></a>How to Manage a CDC Instance
  In questa procedura viene illustrato come utilizzare CDC Designer Console per gestire le operazioni dell'istanza di CDC al runtime.  
  
### <a name="to-manage-cdc-instance-operations"></a>Per gestire le operazioni dell'istanza di CDC  
  
1.  Scegliere **CDC Designer Console** dal menu **Start**.  
  
2.  Nel riquadro sinistro espandere **Change Data Capture** , quindi espandere il servizio che contiene l'istanza che si desidera visualizzare.  
  
3.  Selezionare il nome di un'istanza che si desidera utilizzare.  
  
4.  Nel riquadro **Actions** sul lato destro di CDC Designer Console, fare clic sull'operazione che si desidera eseguire.  
  
     È anche possibile fare clic con il pulsante destro del mouse sul nome dell'istanza nel riquadro sinistro e selezionare l'operazione che si desidera eseguire.  
  
     È possibile eseguire le attività seguenti:  
  
    -   **Avviare**: Per avviare l'acquisizione delle modifiche.  
  
    -   **Arrestare**: Per arrestare l'acquisizione delle modifiche  
  
    -   **Reimpostare**: Fare clic su **Reset** per reimpostare l'istanza di CDC sullo stato iniziale (vuoto). Questa opzione diventa disponibile dopo che l'istanza di CDC è stata interrotta. Tutte le modifiche presenti nelle tabelle delle modifiche e lo stato interno dell'istanza di CDC vengono eliminati. Al successivo avvio dell'istanza di CDC, l'acquisizione delle modifiche verrà avviata da quel momento e includerà solo le transazioni avviate dopo l'avvio dell'istanza di CDC.  
  
    -   **Elimina**: Per eliminare l'istanza di CDC.  
  
    -   **Script di registrazione Oracle**: Fare clic su **Oracle Logging Script** per visualizzare il dialogo Oracle Logging script con lo script di registrazione supplementare Oracle. Per informazioni sulle operazioni che è possibile eseguire in questa finestra di dialogo, vedere [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md).  
  
         **Nota**: Quando si eseguono gli script di registrazione supplementare, viene visualizzata la finestra di dialogo Oracle Credentials for Running Script in cui immettere un nome utente e una password Oracle validi. Per informazioni su come fornire le credenziali Oracle appropriate, vedere [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md).  
  
    -   **CDC Instance Deployment**: Per generare uno script di distribuzione per l'istanza di CDC. Per informazioni su questa finestra di dialogo, vedere [CDC Instance Deployment Script](cdc-instance-deployment-script.md).  
  
     Per ulteriori informazioni su queste attività, vedere [Manage a CDC Instance](manage-a-cdc-instance.md).  
  
 È inoltre possibile selezionare **Properties** per modificare le proprietà di configurazione dell'istanza di CDC. Per ulteriori informazioni sulla modifica delle proprietà dell'istanza di CDC, vedere [Edit Instance Properties](edit-instance-properties.md).  
  
  
