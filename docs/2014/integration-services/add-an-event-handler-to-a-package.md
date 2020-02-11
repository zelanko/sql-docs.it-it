---
title: Aggiungere un gestore eventi a un pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 589d90b52647241b22929473efc9c6e54eb3b75f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062033"
---
# <a name="add-an-event-handler-to-a-package"></a>Aggiunta di un gestore eventi a un pacchetto
  In fase di esecuzione contenitori e attività generano eventi. È possibile creare gestori di eventi personalizzati che rispondono a tali eventi eseguendo un flusso di lavoro alla generazione dell'evento. Ad esempio, è possibile creare un gestore di evento che invia un messaggio di posta elettronica quando un'attività non viene completata correttamente.  
  
 Un gestore di evento è simile a un pacchetto. Come un pacchetto, può fornire un ambito per le variabili e includere un flusso di controllo, oltre a flussi di dati facoltativi. È possibile compilare gestori di eventi per i pacchetti, per il contenitore Ciclo Foreach, per il contenitore Ciclo For, per il contenitore Sequenza e per tutte le attività.  
  
 Per creare i gestori di eventi è possibile usare l'area di progettazione della scheda **Gestori eventi** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 Quando la scheda **Gestori eventi** è attiva, nei nodi **Elementi flusso di controllo** e **Attività di manutenzione** della casella degli strumenti di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] sono disponibili le attività e i contenitori necessari per la compilazione del flusso di controllo del gestore di evento. Nei nodi **Origini flusso di dati**, **Trasformazioni**e **Destinazioni flusso di dati** sono disponibili le origini dei dati, le trasformazioni e le destinazioni per la compilazione dei flussi di dati nel gestore di evento. Per altre informazioni, vedere [Flusso di controllo](control-flow/control-flow.md) e [Flusso di dati](data-flow/data-flow.md).  
  
 La scheda **Gestori eventi** include anche l'area **Gestioni connessioni** , in cui è possibile creare e modificare le gestioni connessioni usate dai gestori di eventi per connettersi a server e origini dei dati. Per altre informazioni, vedere [Creazione di gestioni connessioni](../../2014/integration-services/create-connection-managers.md).  
  
### <a name="to-create-an-event-handler"></a>Per creare un gestore dell'evento  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Gestori eventi** .  
  
     ![Schermata dell'area di progettazione con gestore eventi](media/eventhandlers.gif "Schermata dell'area di progettazione con gestore eventi")  
  
     La creazione del flusso di controllo e dei flussi di dati di un gestore dell'evento è analoga alla creazione del flusso di controllo e dei flussi di dati di un pacchetto. Per altre informazioni, vedere [Flusso di controllo](control-flow/control-flow.md) e [Flusso di dati](data-flow/data-flow.md).  
  
4.  Nell'elenco **File eseguibili** selezionare il file per il quale si desidera creare un gestore dell'evento.  
  
5.  Nell'elenco **Gestore evento** selezionare il gestore dell'evento che si desidera compilare.  
  
6.  Fare clic sul collegamento nell'area di progettazione della scheda **Gestore evento** .  
  
7.  Aggiungere le voci del flusso di controllo nel gestore dell'evento, quindi connetterle tra di loro tramite un vincolo di precedenza trascinando il vincolo da una voce del flusso di controllo a un'altra. Per altre informazioni, vedere [Flusso di controllo](control-flow/control-flow.md).  
  
8.  Facoltativamente, aggiungere un'attività Flusso di dati e nell'area di progettazione della scheda **Flusso di dati** creare un flusso di dati per il gestore dell'evento. Per altre informazioni, vedere [Flusso di dati](data-flow/data-flow.md).  
  
9. Scegliere **Salva elementi selezionati** dal menu **File** per salvare il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Registrazione di Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
