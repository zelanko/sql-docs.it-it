---
title: Abilitare la registrazione in SQL Server Data Tools di pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ef64ee84a90a74d2206fa8cc766e45b1a691566
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66059274"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>Abilitare la registrazione di pacchetti in SQL Server Data Tools
  In questo argomento viene descritta la procedura per aggiungere log in un pacchetto, configurare la registrazione a livello di pacchetto e salvare la configurazione di registrazione in un file XML. È possibile aggiungere log solo a livello di pacchetto. Il pacchetto, tuttavia, non deve eseguire necessariamente la registrazione per consentire la registrazione nei contenitori del pacchetto.  
  
> [!IMPORTANT]  
>  Se si distribuisce il progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , il livello di registrazione impostato per l'esecuzione del pacchetto esegue l'override della registrazione del pacchetto configurata mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Per impostazione predefinita, i contenitori del pacchetto utilizzano la stessa configurazione di registrazione del contenitore padre. Per informazioni sull'impostazione delle opzioni di registrazione per singoli contenitori, vedere [Configurazione della registrazione tramite un file di configurazione salvato](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="to-enable-logging-in-a-package"></a>Per abilitare la registrazione in un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  Scegliere **Registrazione** dal menu **SSIS**.  
  
3.  Selezionare un provider di log nell'elenco **Tipo provider** e quindi fare clic su **Aggiungi**.  
  
4.  Nella colonna **Configurazione** selezionare una gestione connessione oppure fare clic su **\<Nuova connessione>** per creare una nuova gestione connessione del tipo appropriato per il provider di log. A seconda del provider selezionato, utilizzare una delle gestioni connessioni seguenti:  
  
    -   Per file di testo utilizzare una gestione connessione file. Per altre informazioni, vedere [Gestione connessione file](connection-manager/file-connection-manager.md)  
  
    -   Per [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]usare una gestione connessione file.  
  
    -   Per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]utilizzare una gestione connessione OLE DB. Per altre informazioni, vedere [Gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md).  
  
    -   Per il Registro eventi di Windows, non eseguire alcuna operazione. [!INCLUDE[ssIS](../includes/ssis-md.md)] crea automaticamente il registro.  
  
    -   Per file XML utilizzare una gestione connessione file.  
  
5.  Ripetere i passaggi 3 e 4 per ogni log da utilizzare nel pacchetto.  
  
    > [!NOTE]  
    >  In un pacchetto possono venire utilizzati più log di ognuno dei tipi di log.  
  
6.  Facoltativamente, selezionare la casella di controllo a livello di pacchetto, selezionare i log da usare per la registrazione a livello di pacchetto e quindi fare clic sulla scheda **Dettagli** .  
  
7.  Nella scheda **Dettagli** selezionare **Eventi** per registrare tutte le voci di log oppure deselezionare l'opzione **Eventi** se si desidera selezionare singoli eventi.  
  
8.  Facoltativamente, fare clic su **Avanzate** per specificare le informazioni da registrare.  
  
    > [!NOTE]  
    >  Per impostazione predefinita vengono registrate tutte le informazioni.  
  
9. Nella scheda **Dettagli** fare clic su **Salva**. Verrà visualizzata la finestra di dialogo **Salva con nome** . Individuare la cartella in cui salvare la configurazione di registrazione, digitare un nome di file per la nuova configurazione e quindi fare clic su **Salva**.  
  
10. Fare clic su **OK**.  
  
11. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)   
 [Registrazione di Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
