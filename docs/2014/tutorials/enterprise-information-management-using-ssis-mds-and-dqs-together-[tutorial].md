---
title: Enterprise Information Management con SSIS, MDS e DQS insieme [esercitazione] | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: da1804ffec1ffd5e016590e83ac229c9e888ff97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313854"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>Gestione di informazioni aziendali tramite l'utilizzo combinato di SSIS, MDS e DQS [Esercitazione]
  La gestione di informazioni in un'organizzazione comporta in genere l'integrazione dei dati nell'organizzazione e oltre, la pulizia dei dati, la corrispondenza dei dati per rimuovere tutti i duplicati, la standardizzazione e l'arricchimento dei dati, la conformità dei dati anche in termini legali e infine l'archiviazione dei dati in una posizione centralizzata con tutte le impostazioni di sicurezza necessarie.  
  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] sono disponibili tutti i componenti necessari per una soluzione di gestione di informazioni aziendali (EIM, Enterprise Information Management) efficace in un singolo prodotto. Di seguito sono riportati i componenti chiave mediante i quali è possibile compilare una soluzione EIM:  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) offre una piattaforma potente e flessibile per l'integrazione di dati da diverse origini in una soluzione di estrazione, trasformazione e caricamento (ETL, Extract, Transform and Loading) completa che supporta flussi di lavoro aziendali, un data warehouse o la gestione dei dati master. Visualizzare [Cenni preliminari sui servizi di integrazione](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx) argomento per una rapida panoramica e tipici utilizzi di SSIS.  
  
 SQL Server Data Quality Services (DQS) consente la pulizia, la corrispondenza, la standardizzare e l'arricchimento dei dati, pertanto è possibile garantire informazioni attendibili per le funzionalità di Business Intelligence, un data warehouse e carichi di lavoro di elaborazione delle transazioni. Visualizzare [Introduzione a Data Quality Services](https://msdn.microsoft.com/library/ff877917.aspx) argomento per le esigenze aziendali relative a DQS e come DQS risponde alle necessità.  
  
 SQL Server Master Data Services (MDS) fornisce un hub centrale di dati mediante il quale viene garantita l'integrità costante delle informazioni e la coerenza costante dei dati nelle diverse applicazioni. Visualizzare [Panoramica di Master Data Services](../master-data-services/master-data-services-overview-mds.md) argomento per una breve descrizione delle funzionalità importanti di MDS.  
  
 Visualizzare [attività di pulizia e corrispondenza di dati Master tramite tecnologie EIM](https://msdn.microsoft.com/library/hh403491.aspx) white paper per una guida completa sull'implementazione di una soluzione EIM tramite queste tecnologie Microsoft EIM insieme e guarda [Enterprise Gestione delle informazioni (aziendali EIM): Assolutamente innovativo, riunisce SSIS, DQS e MDS](https://go.microsoft.com/fwlink/?LinkId=258672) video per una dimostrazione interessante di uno scenario EIM.  
  
 In questa esercitazione viene illustrato come utilizzare insieme SSIS, MDS e DQS per implementare una soluzione EIM di esempio. Innanzitutto, DQS viene utilizzato per creare una Knowledge Base contenente le informazioni sui dati (metadati), per pulire i dati in un file di Excel utilizzando la Knowledge Base e per far corrispondere i dati in modo da identificare e rimuovere i relativi duplicati. Successivamente, viene utilizzato il componente aggiuntivo MDS per Excel per caricare i dati puliti e corrispondenti in MDS. Infine, l'intero processo viene automatizzato mediante una soluzione SSIS. Tramite la soluzione SSIS in questa esercitazione vengono letti i dati di input da un file di Excel, ma è anche possibile estendere la soluzione per leggere da diverse origini quali Oracle, Teradata, DB2 e il database SQL di Windows Azure.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
1.  Microsoft SQL Server 2012 con i seguenti componenti installati.  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         Visualizzare [Guida all'installazione di SQL Server 2012](../database-engine/install-windows/installation-for-sql-server.md) per informazioni dettagliate sull'installazione del prodotto.  
  
2.  [Configurare MDS tramite Gestione configurazione Master Data Services](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     Utilizzare Gestione configurazione per creare e configurare un database Master Data Services. Dopo aver creato il database MDS, creare un'applicazione web per MDS in un sito web (ad esempio: [ http://localhost/MDS ](http://localhost/MDS)) e associare al database MDS all'applicazione web MDS. Si noti che, per creare un'applicazione Web per MDS, è necessaria l'installazione di IIS nel computer in uso. Visualizzare [requisiti dell'applicazione Web (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx) e [requisiti del Database (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) per informazioni dettagliate sui prerequisiti per la configurazione dell'applicazione web e database MDS.  
  
3.  [Installare e configurare DQS tramite il programma di installazione di Data Quality Server](https://msdn.microsoft.com/library/hh231682.aspx). Fare clic su **avviare**, fare clic su **tutti i programmi**, fare clic su **Microsoft SQL Server 2014**, fare clic su **Data Quality Services**, quindi fare clic su **Programma di installazione di data Quality Server**.  
  
4.  Microsoft Excel 2010 (consigliato a 32 bit).  
  
5.  Installare **componente aggiuntivo Master Data Services per Excel** (32 bit o 64 bit in base alla versione di Excel disponibile nel computer in uso) dalla [qui](https://www.microsoft.com/download/details.aspx?id=29064). Per trovare la versione di Excel sia installato nel computer in uso, eseguire **Excel**, fare clic su **File** sulla barra dei menu e quindi su **Guida** per visualizzare la versione nel riquadro di destra. Si noti che è necessario installare Visual Studio 2010 Tools per Office Runtime prima di installare il componente aggiuntivo di Excel.  
  
6.  (Facoltativo) Creare un account con [Windows Azure Marketplace](https://datamarket.azure.com/). Una delle attività dell'esercitazione richiede un **Azure Marketplace** (denominato originariamente **Data Market**) account. Se lo si desidera, è possibile ignorare questa attività e continuare con la successiva.  
  
7.  Scaricare il file Suppliers. xls [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkId=271504).  
  
8.  DQS non consente di esportare la pulizia o corrispondenza dei risultati in un file di Excel se si usa **versione a 64 bit di Excel**. Questo è un problema noto. Per risolverlo, effettuare le operazioni seguenti:  
  
    1.  Eseguire **DQLInstaller.exe-aggiornamento**. Se è stata installata l'istanza predefinita di SQL Server, il file DQSinstaller.exe è disponibile in C:\Programmi\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn. Fare doppio clic sul file DQSInstaller.exe.  
  
    2.  Nelle **Gestione configurazione Master Data Services**, fare clic su **seleziona Database**selezionare esistente **MDS** del database e quindi fare clic su **aggiornare**.  
  
## <a name="lessons"></a>Lezioni  
  
|Lezione|Breve descrizione|Tempo stimato per il completamento (in minuti)|  
|------------|-----------------------|------------------------------------------------|  
|[Lezione 1: Creazione di Knowledge Base DQS Suppliers.](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|In questa lezione, si crea una knowledge base DQS denominata **Suppliers**.|60|  
|[Lezione 2: Pulizia dei dati fornitore mediante la Knowledge Base Suppliers](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|In questa lezione si creare ed eseguire un progetto DQS per pulire i dati fornitore in un file di Excel utilizzando la **Suppliers** Knowledge Base creata nella prima lezione.|45|  
|[Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|In questa lezione viene creato un progetto DQS per eseguire l'attività di individuazione delle corrispondenze in modo da identificare e rimuovere i duplicati dall'elenco di fornitori con dati puliti.|45|  
|[Lezione 4: Archiviazione dei dati fornitore in MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|In questa lezione è caricare i dati fornitore puliti e corrispondenti a Master Data Services (MDS) tramite il **componente aggiuntivo MDS per Excel**.|45|  
|[Lezione 5: Automatizzazione della pulizia e corrispondenza tramite SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|In questa lezione viene creata una soluzione SSIS mediante la quale vengono puliti i dati di input tramite DQS, viene eseguita la corrispondenza dei dati puliti per rimuovere i duplicati e vengono archiviati i dati puliti e corrispondenti in MDS in modo automatico.|75|  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per iniziare l'esercitazione, passare alla prima lezione: [Lezione 1: Creazione della Knowledge Base DQS Suppliers](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md).  
  
  
