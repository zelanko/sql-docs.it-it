---
title: Scheda gestori eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.eventhandlerwindow.f1
ms.assetid: 94fc8916-8032-490c-b9d5-ded8b6217e49
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4bd7e159a148b134d744481a76ac910af572c0c2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969411"
---
# <a name="event-handlers-tab"></a>Scheda Gestori eventi
  Utilizzare la scheda **Gestori eventi** dello strumento Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per compilare un flusso di controllo in un pacchetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Un gestore di evento viene eseguito in risposta a un evento generato dal pacchetto oppure da un'attività o da un contenitore incluso nel pacchetto.  
  
## <a name="options"></a>Opzioni  
 **File eseguibile**  
 Consente di selezionare il file eseguibile per il quale si desidera compilare un gestore di evento. Il file eseguibile può essere il pacchetto oppure un'attività o un contenitore incluso nel pacchetto.  
  
 **Gestore eventi**  
 Consente di selezionare un gestore di evento. Creare il gestore di evento trascinando gli elementi dalla **casella degli strumenti**.  
  
 **Elimina**  
 Dopo aver selezionato un gestore di evento, fare clic su **Elimina** per rimuoverlo dal pacchetto.  
  
 **Fare clic qui per creare un oggetto \<event handler name> per il file eseguibile\<executable name>**  
 Fare clic per creare il gestore di evento.  
  
 Creare il flusso di controllo trascinando gli oggetti grafici che rappresentano i contenitori e le attività di [!INCLUDE[ssIS](../includes/ssis-md.md)] dalla **casella degli strumenti** all'area di progettazione della scheda **Gestori eventi** e quindi trascinando il connettore per collegare gli oggetti.  
  
 È inoltre possibile fare clic con il pulsante destro del mouse sull'area di progettazione, quindi scegliere **Aggiungi annotazione**dal menu per aggiungere annotazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;i gestori eventi&#41; SSIS](integration-services-ssis-event-handlers.md)   
 [Flusso di controllo](control-flow/control-flow.md)   
 [Progettazione SSIS](ssis-designer.md)   
 [Gestori eventi di Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md)  
  
  
