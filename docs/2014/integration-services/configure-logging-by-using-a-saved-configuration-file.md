---
title: Configurare la registrazione tramite un File di configurazione salvato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- logs [Integration Services], containers
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 605e9f2635ceef0546f4c8e37f74a04a2d27ece0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374369"
---
# <a name="configure-logging-by-using-a-saved-configuration-file"></a>Configurazione della registrazione tramite un file di configurazione salvato
  In questo argomento viene descritta la procedura per configurare la registrazione per nuovi contenitori di un pacchetto semplicemente caricando un file di configurazione della registrazione.  
  
 Per impostazione predefinita, tutti i contenitori di un pacchetto utilizzano la stessa configurazione di registrazione del contenitore padre. Le attività del contenitore Ciclo Foreach, ad esempio, utilizzano la stessa configurazione di registrazione del contenitore.  
  
### <a name="to-configure-logging-for-a-container"></a>Per configurare la registrazione per un contenitore  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  Scegliere **Registrazione** dal menu **SSIS**.  
  
3.  Espandere la visualizzazione albero dei pacchetti e selezionare il contenitore da configurare.  
  
4.  Nella scheda **Provider e log** selezionare i log da usare per il contenitore.  
  
    > [!NOTE]  
    >  È possibile creare log solo a livello di pacchetto. Per altre informazioni, vedere [Abilitare la registrazione di pacchetti in SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md).  
  
5.  Nella scheda **Dettagli** fare clic su **Carica**.  
  
6.  Individuare il file di configurazione della registrazione desiderato e quindi fare clic su **Apri**.  
  
7.  Facoltativamente, selezionare una voce di log diversa selezionando la casella di controllo corrispondente nella colonna **Eventi** . Fare clic su **Avanzate** per selezionare il tipo di informazioni da registrare per tale voce.  
  
    > [!NOTE]  
    >  Il nuovo contenitore potrebbe includere voci di log aggiuntive non disponibili per il contenitore inizialmente utilizzato per creare la configurazione della registrazione. Se si desidera registrare queste voci, è necessario selezionarle in modo manuale.  
  
8.  Per salvare la configurazione della registrazione aggiornata, fare clic su **Salva**.  
  
9. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
