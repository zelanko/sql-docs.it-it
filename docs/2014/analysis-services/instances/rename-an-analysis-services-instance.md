---
title: Rinominare un'istanza di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3ef94fc86c78e896eab03bffb318b58e4b328245
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079615"
---
# <a name="rename-an-analysis-services-instance"></a>Rinominare un'istanza di Analysis Services
  È possibile rinominare un'istanza esistente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tramite il **Rinomina istanza** nella finestra di dialogo.  
  
> [!IMPORTANT]  
>  Mentre si rinomina l'istanza, lo strumento Rinomina istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito con privilegi elevati, aggiornando il nome del servizio Windows, gli account di sicurezza e le voci del Registro di sistema associati a quell'istanza. Per accertarsi che queste azioni vengono effettuate, eseguire questo strumento come amministratore di sistema locale.  
  
 Lo strumento Rinomina istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non modifica la cartella di programma creata per l'istanza originale. Non modificare il nome della cartella di programma in base all'istanza che si sta rinominando. La modifica del nome di una cartella di programma può impedire al programma di installazione di effettuare il ripristino o la disinstallazione di un programma.  
  
> [!NOTE]  
>  L’uso dello strumento Rinomina istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non è supportato in un ambiente cluster.  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>Per rinominare un'istanza di Analysis Services  
  
1.  Avviare il **Rinomina istanza** strumento **asinstancerename.exe**, da C:\Program Files\Microsoft SQL Server\110\Tools\Binn\ManagementStudio.  
  
2.  Nell'elenco **Istanza da rinominare** della finestra di dialogo **Rinomina istanza** selezionare l'istanza che si desidera rinominare.  
  
3.  Immettere il nuovo nome dell'istanza nella casella **Nuovo nome istanza** .  
  
4.  Verificare che il nome utente e la password siano corretti e quindi fare clic su **Rinomina**.  
  
     L'istanza di Analysis Services verrà arrestata e riavviata come parte della modifica del nome.  
  
### <a name="post-rename-checklist"></a>Elenco di controllo successivo alla ridenominazione  
  
1.  Per riprendere l'accesso ai database in esecuzione nell'istanza rinominata, sarà necessario aggiornare manualmente le connessioni dati in Excel o in altre applicazioni client. Verificare inoltre eventuali connessioni predefinite, ad esempio origini dati condivise di Reporting Services, file ODC di Excel o file di connessione BI Semantic Model che potrebbero fare riferimento all'istanza rinominata. Per altre informazioni, vedere [Connetti ad Analysis Services](connect-to-analysis-services.md).  
  
2.  Aggiornare script di PowerShell o script AMO utilizzati regolarmente per eseguire il backup, sincronizzare o elaborare database.  
  
3.  Aggiornare le proprietà del progetto per i progetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usati in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Per le istanze del server in modalità tabulare, accertarsi di aggiornare la proprietà Server dell'area di lavoro nel file con estensione model.bim e la proprietà Server nel progetto.  
  
4.  A seconda di come è stato specificato l'account del servizio, potrebbe essere necessario aggiornare gli account di accesso al database o le autorizzazioni per i file che concedono diritti di accesso ai dati del servizio (ad esempio, se si utilizza l'account del servizio per elaborare dati o accedere a oggetti collegati su un altro server).  
  
     L'aggiornamento di un account di accesso al database o delle autorizzazioni per i file sarà necessario se per il provisioning del servizio è stato utilizzato un account virtuale. Gli account virtuali sono basati sul nome dell'istanza, pertanto se si rinomina l'istanza, verrà aggiornato contemporaneamente anche l'account virtuale. Ciò significa che qualsiasi account di accesso o autorizzazione precedente creata per l'istanza precedente non sarà più valida.  
  
     Di seguito ne viene illustrato un esempio. Si supponga che un server in modalità tabulare è stato installato come istanza denominata "Tabular" tramite l'account virtuale predefinito, causando la configurazione seguente:  
  
    1.  Nome istanza = \<server > \TABULAR  
  
    2.  Nome servizio = MSOLAP$TABULAR  
  
    3.  Account virtuale = NT Service\ MSOLAP$TABULAR  
  
     Ora si supponga che si rinomina l'istanza in "TAB2". Come un risultato della modifica del nome, la configurazione sarà simile alla seguente:  
  
    1.  Nome istanza = \<server > \TAB2  
  
    2.  Nome servizio = MSOLAP$TAB2  
  
    3.  Account virtuale =NT Service\ MSOLAP$TAB2  
  
     Come può notare, le autorizzazioni di database e file concesse precedentemente a "NT Service \ MSOLAP$ TABULAR" non sono più valide. Per garantire che le attività e sulle operazioni eseguite dal servizio eseguite come prima, sarà ora necessario concedere nuove autorizzazioni di database e il file a "NT Service \ MSOLAP$TAB2".  
  
  
