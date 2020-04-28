---
title: Gestione delle informazioni aziendali con SSIS, MDS e DQS insieme [esercitazione] | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487720"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Gestione di informazioni aziendali tramite l'utilizzo combinato di SSIS, MDS e DQS [Esercitazione]
  La gestione di informazioni in un'organizzazione comporta in genere l'integrazione dei dati nell'organizzazione e oltre, la pulizia dei dati, la corrispondenza dei dati per rimuovere tutti i duplicati, la standardizzazione e l'arricchimento dei dati, la conformità dei dati anche in termini legali e infine l'archiviazione dei dati in una posizione centralizzata con tutte le impostazioni di sicurezza necessarie.  
  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] sono disponibili tutti i componenti necessari per una soluzione di gestione di informazioni aziendali (EIM, Enterprise Information Management) efficace in un singolo prodotto. Di seguito sono riportati i componenti chiave mediante i quali è possibile compilare una soluzione EIM:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   Master Data Services di SQL Server  
  
 SQL Server Integration Services (SSIS) offre una piattaforma potente e flessibile per l'integrazione di dati da diverse origini in una soluzione di estrazione, trasformazione e caricamento (ETL, Extract, Transform and Loading) completa che supporta flussi di lavoro aziendali, un data warehouse o la gestione dei dati master. Per una rapida panoramica e per gli usi tipici di SSIS, vedere l'argomento [Integration Services Overview](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) .  
  
 SQL Server Data Quality Services (DQS) consente la pulizia, la corrispondenza, la standardizzare e l'arricchimento dei dati, pertanto è possibile garantire informazioni attendibili per le funzionalità di Business Intelligence, un data warehouse e carichi di lavoro di elaborazione delle transazioni. Vedere l'argomento [Introduzione a Data Quality Services](https://msdn.microsoft.com/library/ff877917.aspx) per le esigenze aziendali di DQS e il modo in cui DQS risponde alle esigenze.  
  
 SQL Server Master Data Services (MDS) fornisce un hub centrale di dati mediante il quale viene garantita l'integrità costante delle informazioni e la coerenza costante dei dati nelle diverse applicazioni. Vedere l'argomento [Master Data Services Panoramica](../master-data-services/master-data-services-overview-mds.md) per brevi descrizioni delle funzionalità importanti di MDS.  
  
 Per informazioni complete sull'implementazione di una soluzione EIM tramite queste tecnologie Microsoft EIM, vedere la pagina relativa alla [pulizia e alla corrispondenza dei dati master tramite le tecnologie EIM](https://msdn.microsoft.com/library/hh403491.aspx) white paper e guardare la pagina relativa alla [gestione delle informazioni aziendali (EIM): riunire i video SSIS, DQS e MDS](https://go.microsoft.com/fwlink/?LinkId=258672) per una dimostrazione interessante di uno scenario EIM.  
  
 In questa esercitazione viene illustrato come utilizzare insieme SSIS, MDS e DQS per implementare una soluzione EIM di esempio. Innanzitutto, DQS viene utilizzato per creare una Knowledge Base contenente le informazioni sui dati (metadati), per pulire i dati in un file di Excel utilizzando la Knowledge Base e per far corrispondere i dati in modo da identificare e rimuovere i relativi duplicati. Successivamente, viene utilizzato il componente aggiuntivo MDS per Excel per caricare i dati puliti e corrispondenti in MDS. Infine, l'intero processo viene automatizzato mediante una soluzione SSIS. La soluzione SSIS in questa esercitazione legge i dati di input da un file di Excel, ma è possibile estenderli per leggere da diverse origini, ad esempio Oracle, Teradata, DB2 e il database SQL di Azure.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
1.  Microsoft SQL Server 2012 con i seguenti componenti installati.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Per informazioni dettagliate sull'installazione del prodotto, vedere la [Guida all'installazione di SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) .  
  
2.  [Configurare MDS tramite Gestione configurazione Master Data Services](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     Utilizzare Gestione configurazione per creare e configurare un database Master Data Services. Dopo aver creato il database MDS, creare un'applicazione Web per MDS in un sito Web (ad esempio, `http://localhost/MDS`) e associare il database MDS all'applicazione Web MDS. Si noti che, per creare un'applicazione Web per MDS, è necessaria l'installazione di IIS nel computer in uso. Per informazioni dettagliate sui prerequisiti per la configurazione del database MDS e dell'applicazione Web, vedere Requisiti [dell'applicazione Web (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx) e [requisiti del database (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) .  
  
3.  [Installare e configurare DQS utilizzando il programma di installazione di Data Quality Server](https://msdn.microsoft.com/library/hh231682.aspx). Fare clic sul pulsante **Start**, scegliere **tutti i programmi**, **Microsoft SQL Server 2014**, fare clic su **Data Quality Services**, quindi su **programma di installazione di Data Quality Server**.  
  
4.  Microsoft Excel 2010 (consigliato a 32 bit).  
  
5.  Installare **componente aggiuntivo Master Data Services per Excel** (32 bit o 64 bit in base alla versione di Excel disponibile nel computer in uso) da [qui](https://www.microsoft.com/download/details.aspx?id=29064). Per trovare la versione di Excel installata nel computer, eseguire **Excel**, fare clic su **file** nella barra dei menu e fare **clic su? per visualizzare** la versione nel riquadro destro. Si noti che è necessario installare Visual Studio 2010 Tools per Office Runtime prima di installare il componente aggiuntivo di Excel.  
  
6.  Opzionale Creare un account con [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/). Per una delle attività dell'esercitazione è necessario disporre di un account di **Azure Marketplace** (originariamente denominato **Data Market**). Se lo si desidera, è possibile ignorare questa attività e continuare con la successiva.  
  
7.  Scaricare il file Suppliers. xls dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=50426).  
  
8.  DQS non consente di esportare i risultati di pulizia o di corrispondenza in un file di Excel se si utilizza la **versione a 64 bit di Excel**. Questo è un problema noto. Per risolverlo, effettuare le operazioni seguenti:  
  
    1.  Eseguire **DQLInstaller. exe-upgrade**. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe è disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Fare doppio clic sul file DQSInstaller.exe.  
  
    2.  In **Gestione configurazione Master Data Services**fare clic su **Seleziona database**, selezionare database **MDS** esistente e quindi fare clic su **Aggiorna**.  
  
## <a name="lessons"></a>Lezioni  
  
|Lezione|Breve descrizione|Tempo stimato per il completamento (in minuti)|  
|------------|-----------------------|------------------------------------------------|  
|[Lezione 1: Creazione di una Knowledge Base DQS Suppliers](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|In questa lezione verrà creata una Knowledge Base DQS denominata **Suppliers**.|60|  
|[Lezione 2: Pulizia dei dati fornitore tramite la Knowledge Base Suppliers](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|In questa lezione viene creato ed eseguito un progetto DQS per pulire i dati fornitore in un file di Excel utilizzando la Knowledge base **Suppliers** creata nella prima lezione.|45|  
|[Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|In questa lezione viene creato un progetto DQS per eseguire l'attività di individuazione delle corrispondenze in modo da identificare e rimuovere i duplicati dall'elenco di fornitori con dati puliti.|45|  
|[Lezione 4: Archiviazione dei dati fornitore in MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|In questa lezione vengono caricati i dati fornitore puliti e corrispondenti a Master Data Services (MDS) usando il **componente aggiuntivo MDS per Excel**.|45|  
|[Lezione 5: Automazione della pulizia e della corrispondenza tramite SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|In questa lezione viene creata una soluzione SSIS mediante la quale vengono puliti i dati di input tramite DQS, viene eseguita la corrispondenza dei dati puliti per rimuovere i duplicati e vengono archiviati i dati puliti e corrispondenti in MDS in modo automatico.|75|  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per iniziare l'esercitazione, passare alla prima lezione: [lezione 1: creazione della Knowledge Base DQS Suppliers](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
