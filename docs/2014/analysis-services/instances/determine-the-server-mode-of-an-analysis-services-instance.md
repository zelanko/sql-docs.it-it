---
title: Determinare la modalità Server di analisi Services istanza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e556fb1-ca37-4f06-8f8f-f187cb0fdb37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff9ac19c0b605266de5eca69dd0f410f0d8fbdd2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080055"
---
# <a name="determine-the-server-mode-of-an-analysis-services-instance"></a>Determinare la modalità server di un'istanza di Analysis Services
  Analysis Services può essere installato in una delle tre modalità server: Multidimensionale e Data Mining (impostazione predefinita), PowerPivot per SharePoint e tabulare. La modalità server di un'istanza di Analysis Services è determinata durante l'installazione quando si scelgono le opzioni per l'installazione del server.  
  
 La modalità server determina il tipo di soluzione creata e distribuita. Se non è stato installato il software server e si desidera sapere in quale modalità è stato installato il server, è possibile usare le informazioni di questo argomento per determinare tale modalità. Per altre informazioni sulla disponibilità delle funzionalità in una modalità specifica, vedere [Confronto tra soluzioni tabulari e multidimensionali &#40;SSAS&#41;](../comparing-tabular-and-multidimensional-solutions-ssas.md).  
  
 Se non si desidera usare la modalità server installata, è necessario disinstallare e reinstallare il software, scegliendo la modalità preferita. In alternativa, è possibile installare un'istanza aggiuntiva di Analysis Services nello stesso computer per disporre di più istanze eseguite in modalità diverse.  
  
## <a name="server-icons-in-object-explorer"></a>Icone del server in Esplora oggetti  
 Il modo più semplice per determinare la modalità server consiste nel connettersi al server in SQL Server Management Studio e individuare l'icona accanto al nome del server in Esplora oggetti. Nell'illustrazione seguente vengono mostrate tre istanze di Analysis Services distribuite in modalità multidimensionale, tabulare e PowerPivot:  
  
 ![Icone Esplora oggetti per ogni modalità server](../media/ssas-ssms-servermodes.gif "icone di Esplora oggetti per ogni modalità server")  
  
## <a name="viewing-deploymentmode-property-in-msmdsrvini-file"></a>Visualizzazione della proprietà DeploymentMode nel file MSMDSRV.INI  
 In alternativa, è possibile verificare la proprietà `DeploymentMode` nel file msmdsrv.ini incluso in ogni istanza di Analysis Services. Il valore di questa proprietà identifica la modalità del server. I valori validi sono 0 (multidimensionale), 1 (SharePoint) o 2 (tabulare). Per aprire il file msmdsrv.ini, è necessario essere un amministratore (ovvero, un membro del ruolo server) di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questo file contiene XML strutturato. È possibile visualizzare il file usando Blocco note o qualsiasi editor di testo.  
  
> [!CAUTION]  
>  Non modificare il valore della proprietà `DeploymentMode`. La modifica manuale della proprietà dopo l'installazione del server non è supportata.  
  
## <a name="about-the-deploymentmode-property"></a>Informazioni sulla proprietà DeploymentMode  
 La proprietà `DeploymentMode` consente di determinare il contesto operativo di un'istanza del server Analysis Services. Questa proprietà è definita 'modalità server' in finestre di dialogo, messaggi e documentazione. Questa proprietà viene inizializzata dal programma di installazione in base alla modalità di installazione di Analysis Services e deve essere considerata solo per uso interno, usando sempre il valore specificato dal programma di installazione.  
  
 Tra i valori validi per questa proprietà sono inclusi i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Rappresenta il valore predefinito. Specifica la modalità multidimensionale, usata per i database multidimensionali che usano l'archiviazione MOLAP, HOLAP e ROLAP, nonché i modelli di data mining.|  
|1|Consente di specificare le istanze di Analysis Services installate come parte di una distribuzione di PowerPivot per SharePoint. Non modificare la proprietà della modalità di distribuzione dell'istanza di Analysis Services che è parte di un'installazione di PowerPivot per SharePoint. I dati PowerPivot non verranno più eseguiti nel server se si cambia modalità.|  
|2|Specifica la modalità tabulare usata per l'hosting dei database del modello tabulare che usano l'archiviazione in memoria o DirectQuery.|  
  
 Ogni modalità comporta l'esclusione dell'altra. In un server configurato per la modalità tabulare non è possibile eseguire i database di Analysis Services che contengono cubi e dimensioni. Se l'hardware del computer sottostante può supportare tale condizione, è possibile installare più istanze di Analysis Services nello stesso computer e configurare ogni istanza per l'utilizzo di una modalità di distribuzione diversa. Analysis Services è un'applicazione a elevato utilizzo di risorse. La distribuzione di più istanze sullo stesso sistema viene consigliata solo per server di fascia alta.  
  
## <a name="see-also"></a>Vedere anche  
 [Installare Analysis Services in modalità tabulare](install-windows/install-analysis-services.md)   
 [Installazione di Analysis Services in modalità Multidimensionale e Data Mining](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [Installazione PowerPivot per SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Connetti ad Analysis Services](connect-to-analysis-services.md)   
 [Soluzioni di modelli tabulari &#40;SSAS tabulare&#41;](../tabular-model-solutions-ssas-tabular.md)   
 [Soluzioni di modelli multidimensionali &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Modelli di data mining &#40;Analysis Services - Data mining&#41;](../data-mining/mining-models-analysis-services-data-mining.md)  
  
  
