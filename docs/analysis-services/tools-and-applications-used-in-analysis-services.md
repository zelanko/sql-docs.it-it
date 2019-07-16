---
title: Strumenti e applicazioni usate in Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d3ecb5de4c70c09bc367b9008f5d62c6a23faef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162291"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Strumenti e applicazioni usati in Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Scopri gli strumenti e le applicazioni che necessari per la creazione di modelli di Analysis Services e la gestione di database distribuiti.  
  
## <a name="analysis-services-model-designers"></a>Strumenti di progettazione dei modelli di Analysis Services  
 I modelli vengono creati usando i modelli di progetto in SQL Server Data Tools (SSDT), una shell di Visual Studio. Modelli di progetto forniscono i progettisti di modelli per la creazione degli oggetti del modello di dati che costituiscono una soluzione di Analysis Services. SSDT è disponibile come download web gratuito aggiornato ogni mese.

 **[Scaricare SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 I modelli usano un'impostazione del livello di compatibilità per determinare la disponibilità di funzionalità e la versione di Analysis Services che deve eseguire il modello.  Se è possibile specificare che un determinato livello di compatibilità viene determinato in parte dalla finestra di progettazione del modello.  
  
 Modelli tabulari utilizzando le funzionalità più recenti, ad esempio i file BIM in formato JSON tabulare e bidirezionale il filtro incrociato, devono essere creati o aggiornati a livello di compatibilità 1200 o superiore.  
  
 Se è necessario un livello di compatibilità inferiore, forse perché si vuole distribuire un modello in una versione precedente di Analysis Services, è possibile comunque utilizzare la finestra di progettazione del modello in SSDT. Le versioni più recenti dello strumento supportano la creazione di qualsiasi tipo di modello tabulare o multidimensionale, a qualsiasi livello di compatibilità.   

## <a name="administrative-tools"></a>Strumenti di amministrazione  
  
 SQL Server Management Studio (SSMS) è lo strumento di amministrazione principale per tutte le funzionalità di SQL Server, inclusi Analysis Services. SSMS è un download web gratuito aggiornato ogni mese. 
  
**[Scaricare SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SQL Server Management Studio include gli eventi estesi (XEvent), che fornisce un'alternativa semplificata alle tracce di SQL Server Profiler usati per attività di monitoraggio e diagnosi di problemi in SQL Server 2016 e server Azure Analysis Services. Per altre informazioni, vedere [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 Sebbene sia ufficialmente deprecato a favore di xEvents, SQL Server Profiler consente di monitorare facilmente connessioni, esecuzione di query MDX e altre operazioni del server. SQL Server Profiler viene installato per impostazione predefinita. È possibile trovarlo con le applicazioni di SQL Server per le App in Windows.  
  
### <a name="powershell"></a>PowerShell  
 È possibile usare i comandi PowerShell per eseguire molte attività amministrative. Visualizzare [riferimento a PowerShell](../analysis-services/powershell/analysis-services-powershell-reference.md) per altre informazioni.  
  
### <a name="community-and-third-party-tools"></a>Strumenti della community e di terze parti  
 Controllare la [pagina codeplex di Analysis Services](http://sqlsrvanalysissrvcs.codeplex.com/) per esempi di codice della community. I[forum](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) possono essere utili per cercare consigli sugli strumenti di terze parti che supportano Analysis Services.  
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità di un Database multidimensionale](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Livello di compatibilità per i modelli tabulari](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
