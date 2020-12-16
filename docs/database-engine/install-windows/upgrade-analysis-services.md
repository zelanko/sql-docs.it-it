---
description: Aggiornare Analysis Services
title: Aggiornare Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 12/09/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
monikerRange: '>=sql-server-2016'
manager: erikre
ms.openlocfilehash: 73258d31f23c52915319aa765dd8d9bcbb7f2e35
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480352"
---
# <a name="upgrade-analysis-services"></a>Aggiornare Analysis Services

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  Le istanze di Analysis Services possono essere aggiornate a una versione di SQL Server con la stessa modalità server per sfruttare i vantaggi delle funzionalità introdotte nella versione corrente, come descritto in [Novità di Analysis Services](/analysis-services/what-s-new-in-analysis-services).  
  
 È possibile aggiornare ogni istanza sul posto, indipendentemente dalle altre istanze in esecuzione sullo stesso hardware. Tuttavia, la maggior parte degli amministratori sceglie di installare una nuova istanza della nuova versione per il testing dell'applicazione prima di trasferire i carichi di lavoro sul nuovo server. Per i server di sviluppo o test, potrebbe essere più opportuno un aggiornamento sul posto.  
  
## <a name="server-upgrade"></a>Aggiornamento del server  
 Esistono due approcci di base per l'aggiornamento di server e database:  
  
> [!NOTE]
> I livelli di compatibilità dei database collegati a un determinato server rimangono invariati, a meno che non vengano modificati manualmente.
   
  
### <a name="in-place-upgrade"></a>Aggiornamento sul posto  
 Il processo di aggiornamento esegue automaticamente la migrazione dei database esistenti dall'istanza precedente alla nuova istanza. Poiché i metadati e i dati binari sono compatibili tra le due versioni, i dati verranno mantenuti in seguito all'aggiornamento e non sarà necessario eseguirne la migrazione manuale.  
  
 Per aggiornare un'istanza esistente, eseguire il programma di installazione e specificare il nome dell'istanza esistente come nome della nuova istanza.  
  
### <a name="side-by-side-upgrade"></a>Aggiornamento affiancato  
  
-   Eseguire il backup di tutti i database e verificare che ognuno di essi possa essere ripristinato. Per altre informazioni, vedere [Backup e ripristino di database di Analysis Services](/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases).  
  
-   Identificare un subset di report, fogli di calcolo o snapshot del dashboard da usare successivamente come base di verifica delle operazioni del server dopo l'aggiornamento. Se possibile, raccogliere misure delle prestazioni in modo da confrontare i carichi di lavoro sul server aggiornato.  
  
-   Installare una nuova istanza di Analysis Services, scegliendo la stessa modalità del server (tabulare o multidimensionale) attiva sul server da sostituire. 
  
     Attività successive all'installazione per la configurazione di porte e l'aggiunta di amministratori del server. Per altre informazioni, vedere [Configurazione successiva all'installazione &#40;Analysis Services&#41;](/analysis-services/instances/post-install-configuration-analysis-services).  
  
-   Collegare o ripristinare ogni database.  
  
-   Eseguire DBCC per verificare l'integrità del database. Sui modelli tabulari è possibile eseguire un controllo più accurato, con test per gli oggetti orfani presenti nell'intera gerarchia del modello. Sui modelli multidimensionali, vengono controllati solo gli indici di partizione. Per altre informazioni, vedere [Database Consistency Checker &#40;DBCC&#41; per i database tabulari e multidimensionali di Analysis Services](/analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services).  
  
-   Report dei test, fogli di calcolo e dashboard per accertarsi che non si sono verificati cambiamenti in negativo nel comportamento o nei calcoli. Si dovrebbero riscontrare prestazioni più veloci sia per i carichi di lavoro multidimensionali che per quelli tabulari.  
  
-   Verificare le operazioni di elaborazione, correggendo eventuali problemi di accesso o autorizzazione. Se si usa l'account predefinito del servizio per le connessioni, il nuovo servizio viene eseguito con un account diverso. Per altre informazioni, vedere [Configurare gli account del servizio &#40;Analysis Services&#41;](/analysis-services/instances/configure-service-accounts-analysis-services).  
  
-   Verificare il backup e ripristinare le operazioni nel server aggiornato, regolando gli script per l'uso con il nuovo nome del server.  
  
## <a name="database-upgrade"></a>Aggiornamento del database  
 I database creati in versioni precedenti vengono eseguiti nel server aggiornato con l'impostazione del livello di compatibilità originale. In genere, è possibile aggiornare un database o un modello a un livello di compatibilità più elevato per ottenere l'accesso alle nuove funzionalità, ma questa operazione vincola l'utente a una versione specifica del server.  
  
 Per aggiornare un database, in genere si aggiorna il modello in SQL Server Data Tools (SSDT) e quindi si distribuisce la soluzione a un'istanza del server aggiornato.
  
 I database tabulari e multidimensionali seguono percorsi di versione diversi. È un caso che i modelli multidimensionali e i modelli tabulari abbiano livelli di compatibilità molto simili.  Le modalità avanzeranno a velocità diverse se le modifiche alle funzionalità influiscono solo uno di questi database.  
  
 Per motivi di background, nella tabella seguente sono riepilogati i livelli di compatibilità, ma è necessario esaminare gli articoli specifici per conoscere le caratteristiche di ogni livello.  
  
|Modello di database|Livello di compatibilità|Versioni compatibili|  
|-|-|-|  
|Tabulare|1500|SQL Server 2019|
|Tabulare|1400|SQL Server 2017|
|Tabulare|1200|SQL Server 2016|  
|Tabulare|1103|SQL Server 2014|  
|Tabulare|1100|SQL Server 2012|  
|Multidimensionale|1100|SQL Server 2012 e versioni successive|  
|Multidimensionale|1050|SQL Server 2005, 2008, 2008 R2|  
  
 Per altre informazioni, vedere [Livello di compatibilità di un database multidimensionale &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services) e [Livello di compatibilità per i modelli tabulari di Analysis Services](/analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services).  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Aggiornare Power Pivot per SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
