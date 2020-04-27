---
title: Sincronizzare Analysis Services database | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, Synchronize Database Wizard
- deploying [Analysis Services], Synchronize Database Wizard
- Synchronize Database Wizard
- synchronization [Analysis Services]
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a561b348b30afcbfe5305681f56e4f8314fa510
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072845"
---
# <a name="synchronize-analysis-services-databases"></a>Sincronizzare database di Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include una funzionalità di sincronizzazione database che consente di rendere due database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] equivalenti, copiando i dati e i metadati di un database situato su un server di origine in‌ un altro database situato su un server di destinazione. Utilizzare la funzionalità Sincronizzazione database per completare le attività seguenti:  
  
-   Distribuire un database da un server temporaneo in un server di produzione.  
  
-   Aggiornare un database su un server di produzione con le modifiche apportate ai dati e metadati in un database su un server temporaneo.  
  
-   Generare uno script XMLA che possa essere eseguito successivamente per sincronizzare i database.  
  
-   Nei carichi di lavoro distribuiti in cui i cubi e le dimensioni vengono elaborati in più server, utilizzare la sincronizzazione database per unire le modifiche in un singolo database.  
  
 La sincronizzazione database viene avviata nel server di destinazione, effettuando il pull dei dati e dei metadati in una copia del database nel server di origine. Se il database non esiste, verrà creato. La sincronizzazione è un'operazione occasionale e unidirezionale che termina dopo la copia del database. Non fornisce la parità in tempo reale tra i database.  
  
 È possibile risincronizzare i database già esistenti nei server di origine e destinazione per effettuare il pull delle modifiche più recenti da un server temporaneo in un database di produzione. Verrà eseguito un confronto dei file presenti nei due server per verificarne le modifiche e i file diversi verranno aggiornati. I database esistenti nel server di destinazione rimarranno disponibili durante la sincronizzazione in background. Gli utenti possono continuare a eseguire query sul database di destinazione durante la sincronizzazione. Al termine della sincronizzazione, tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gli utenti vengono trasferiti automaticamente ai dati e metadati appena copiati e vengono eliminati i vecchi dati dal database di destinazione.  
  
 Per sincronizzare i database, eseguire la sincronizzazione guidata database per sincronizzare immediatamente i database oppure per generare uno script di sincronizzazione che è possibile eseguire successivamente. Entrambi gli approcci possono essere utilizzati per aumentare la disponibilità e la scalabilità del cubo e dei database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  I seguenti white paper, scritti per le versioni precedenti di Analysis Services, rimangano validi per le soluzioni multidimensionali scalabili compilate con SQL Server 2012. Per altre informazioni, vedere [Scale-Out Querying with Analysis Services](https://go.microsoft.com/fwlink/?LinkId=253136) (Scalabilità orizzontale delle query con Analysis Services) e [Scale-Out Querying for Analysis Services with Read-Only Databases](https://go.microsoft.com/fwlink/?LinkId=253137.)(Scalabilità orizzontale delle query per Analysis Services con i database di sola lettura)  
  
## <a name="prerequisites"></a>Prerequisiti  
 Nel server di destinazione da cui viene avviata la sincronizzazione del database, è necessario essere un membro del ruolo di amministratore del server Analysis Services. Nel server di origine, l'account utente di Windows deve disporre di autorizzazioni Controllo completo sul database di origine. Se si esegue la sincronizzazione del database in modo interattivo, tenere presente che la sincronizzazione viene eseguita nel contesto di sicurezza dell'identità utente di Windows. Se all'account viene negato l'accesso a oggetti specifici, tali oggetti verranno esclusi dall'operazione. Per ulteriori informazioni sui ruoli di amministratore del server e le autorizzazioni di database, vedere concedere le autorizzazioni di [amministratore del server &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) e [concedere autorizzazioni per il database &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md).  
  
 La porta TCP 2383 deve essere aperta in entrambi i server per consentire le connessioni remote tra le istanze predefinite. Per altre informazioni sulla creazione di un'eccezione in Windows Firewall, vedere [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Sia il server di origine che quello di destinazione devono avere la stessa versione e Service Pack. Poiché anche i metadati del modello sono sincronizzati, per garantire la compatibilità il numero di build per entrambi i server deve essere lo stesso. L'edizione di ogni installazione deve supportare la sincronizzazione del database. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]la sincronizzazione del database è supportata nelle edizioni Enterprise, Developer e Business Intelligence. Per ulteriori informazioni sulle funzionalità di ogni edizione, vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 La modalità di distribuzione server deve essere identica in ogni server. Se il database che si sta sincronizzando è multidimensionale, è necessario che sia il server di origine che quello di destinazione siano configurati per la modalità server multidimensionale. Per altre informazioni sulle modalità di distribuzione, vedere [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Disattivare l'elaborazione lenta delle aggregazioni se viene utilizzate nel server di origine. Le aggregazioni che vengono elaborate in background possono interferire con la sincronizzazione del database. Per altre informazioni sull'impostazione di questa proprietà server, vedere [Proprietà OLAP](../server-properties/olap-properties.md).  
  
> [!NOTE]  
>  La dimensione del database rappresentano un fattore determinante nello stabilire se la sincronizzazione è un approccio appropriato. Non esistono requisiti hardware, ma se la sincronizzazione è troppo lenta, provare a sincronizzare più server in parallelo, come descritto nella documentazione tecnica seguente: [Analysis Services Synchronization Best Practices](https://go.microsoft.com/fwlink/?LinkID=253136)(Procedure consigliate per la sincronizzazione di Analysis Services).  
  
## <a name="synchronize-database-wizard"></a>Sincronizzazione guidata database  
 Utilizzare la Sincronizzazione guidata database per eseguire la sincronizzazione unidirezionale da un database di origine a un database di destinazione o per generare uno script che specifica un'operazione di sincronizzazione del database. Durante il processo di sincronizzazione è possibile sincronizzare sia le partizioni remote che quelle locali nonché scegliere se includere i ruoli.  
  
 Sincronizzazione guidata database consente di eseguire in modo semplificato i passaggi seguenti:  
  
-   Selezionare l'istanza di origine e il database da cui eseguire la sincronizzazione.  
  
-   Selezionare le posizioni di archiviazione per le partizioni locali nell'istanza di destinazione.  
  
-   Selezionare le posizioni di archiviazione per le partizioni remote in altre istanze di destinazione.  
  
-   Selezionare il livello di sicurezza e le informazioni sull'appartenenza da copiare dall'istanza e dal database di origine nell'istanza di destinazione.  
  
-   Scegliere se eseguire immediatamente la sincronizzazione o se salvare il comando **Synchronize** XMLA (XML for Analysis) generato dalla Sincronizzazione guidata database in un file script per eseguire il processo in un secondo momento.  
  
 Per impostazione predefinita, la procedura guidata consente di sincronizzare tutti i dati e i metadati, tranne i dati di appartenenza situati in gruppi di sicurezza esistenti. Quando si sincronizzano i dati e i metadati, è anche possibile copiare tutte le impostazioni di sicurezza o ignorarle.  
  
#### <a name="run-the-wizard"></a>Eseguire la procedura guidata  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui verrà eseguito il database di destinazione. Se ad esempio si distribuisce un database in un server di produzione, eseguire la procedura guidata nel server di produzione.  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla cartella **Database** , quindi scegliere **Sincronizza**.  
  
3.  Specificare il nome del server di origine e del database di origine. Nella pagina Selezione database da sincronizzare digitare il nome del server di origine e del database di origine in **Server di origine** e **Database di origine**. Se ad esempio si esegue la distribuzione da un ambiente di testing a un server di produzione, l'origine sarà il database nel server temporaneo.  
  
     In**Server di destinazione** viene visualizzato il nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con cui vengono sincronizzati i dati e i metadati dal database selezionato in **Database di origine** .  
  
     Verrà eseguita la sincronizzazione per i database di origine e di destinazione aventi lo stesso nome. Se il server di destinazione dispone già di un database che condivide lo stesso nome del database di origine, il database di destinazione sarà aggiornato con i metadati e i dati dell'origine. Se il database non esiste, verrà creato nel server di destinazione.  
  
4.  Facoltativamente, modificare il percorso della partizione locale. Usare la pagina **Impostazione percorsi partizioni locali** per indicare il percorso in cui archiviare le partizioni locali nel server di destinazione.  
  
    > [!NOTE]  
    >  Questa pagina viene visualizzata solo se nel database specificato esiste almeno una partizione locale.  
  
     Se sull'unità C del server di origine è installato un set di partizioni, la procedura guidata consente di copiare questo set di partizioni in una posizione diversa nel server di destinazione. Se le posizioni predefinite non vengono modificate, la procedura guidata distribuisce le partizioni del gruppo di misure situate all'interno di ciascun cubo del server di origine nelle stesse posizioni del server di destinazione. Analogamente, se nel server di origine vengono utilizzate partizioni remote, sul server di destinazione verranno utilizzate le medesime partizioni remote.  
  
     L'opzione **Percorsi** consente di visualizzare una griglia in cui sono elencate la cartella di origine, la cartella di destinazione e le dimensioni stimate delle partizioni locali da archiviare nell'istanza di destinazione. La griglia include le colonne seguenti:  
  
     **Cartella di origine**  
     Consente di visualizzare il nome della cartella nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di origine contenente la partizione remota. Se nella colonna è incluso il valore "(Impostazione predefinita)", la partizione locale è contenuta nel percorso predefinito relativo all'istanza di origine.  
  
     **Cartella di destinazione**  
     Consente di visualizzare il nome della cartella dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di destinazione in cui sincronizzare la partizione locale. Se nella colonna è incluso il valore "(Impostazione predefinita)", la partizione locale è contenuta nel percorso predefinito relativo all'istanza di destinazione.  
  
     Fare clic sui puntini di sospensione (**...**) per visualizzare la finestra di dialogo **Cerca cartella remota** e specificare una cartella nell'istanza di destinazione all'interno della quale sincronizzare le partizioni locali archiviate nel percorso selezionato.  
  
    > [!NOTE]  
    >  Non è possibile modificare questa colonna per le partizioni locali archiviate nel percorso predefinito relativo all'istanza di origine.  
  
     **Dimensione**  
     Consente di visualizzare le dimensioni stimate della partizione locale.  
  
     L'opzione **Partizioni nel percorso selezionato** consente di visualizzare una griglia in cui vengono descritte le partizioni locali archiviate nel percorso dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di origine specificata nella colonna **Cartella di origine** della riga selezionata in **Percorsi**.  
  
     **Cubo**  
     Consente di visualizzare il nome del cubo contenente la partizione.  
  
     **Gruppo di misure**  
     Consente di visualizzare il nome del gruppo di misure del cubo contenente la partizione.  
  
     **Nome partizione**  
     Consente di visualizzare il nome della partizione.  
  
     **Dimensioni (MB)**  
     Consente di visualizzare le dimensioni in megabyte della partizione.  
  
5.  Facoltativamente, modificare il percorso delle partizioni remote. Usare la pagina **Impostazione percorsi partizioni remote** per indicare se le partizioni remote gestite dal database specificato nel server di origine devono essere sincronizzate e per specificare un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di destinazione e un database in cui archiviare le partizioni remote selezionate.  
  
    > [!NOTE]  
    >  Questa pagina viene visualizzata solo se almeno una partizione remota viene gestita dal database specificato nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di origine.  
  
     L'opzione **Percorsi** consente di visualizzare una griglia nella quale vengono elencate informazioni dettagliate sui percorsi in cui vengono archiviate le partizioni remote per il database di origine, incluse informazioni sulla destinazione e l'origine e le dimensioni di archiviazione usate da ogni percorso, disponibili dal database selezionato. La griglia include le colonne seguenti:  
  
     **Sincronizza**  
     Selezionare questa opzione per includere un percorso contenente le partizioni remote durante la sincronizzazione.  
  
    > [!NOTE]  
    >  Se non si seleziona questa opzione per un percorso, le partizioni remote incluse in quest'ultimo non verranno sincronizzate.  
  
     **Server di origine**  
     Consente di visualizzare il nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente le partizioni remote.  
  
     **Cartella di origine**  
     Consente di visualizzare il nome della cartella nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente le partizioni remote. Se nella colonna è incluso il valore "(Impostazione predefinita)", le partizioni remote saranno presenti nella posizione predefinita relativa all'istanza visualizzata in **Server di origine** .  
  
     **Server di destinazione**  
     Consente di visualizzare il nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno della quale devono essere sincronizzate le partizioni remote archiviate nel percorso specificato in **Server di origine** e **Cartella di origine** .  
  
     Fare clic sui puntini di sospensione (**...**) per visualizzare la finestra di dialogo **Gestione connessione** e specificare un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui sincronizzare le partizioni remote archiviate nel percorso specificato.  
  
     **Cartella di destinazione**  
     Consente di visualizzare il nome della cartella dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di destinazione in cui sincronizzare la partizione remota. Se nella colonna è incluso il valore "(Impostazione predefinita)", la partizione remota è contenuta nel percorso predefinito relativo all'istanza di destinazione.  
  
     Fare clic sui puntini di sospensione (**...**) per visualizzare la finestra di dialogo **Cerca cartella remota** e specificare una cartella nell'istanza di destinazione all'interno della quale sincronizzare le partizioni remote archiviate nel percorso selezionato.  
  
     **Dimensione**  
     Consente di visualizzare le dimensioni stimate delle partizioni remote archiviate nel percorso.  
  
     L'opzione **Partizioni nel percorso selezionato** consente di visualizzare una griglia in cui vengono descritte le partizioni remote archiviate nel percorso dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] di origine specificata nella colonna **Cartella di origine** della riga selezionata in **Percorsi**. La griglia include le colonne seguenti:  
  
     **Cubo**  
     Consente di visualizzare il nome del cubo contenente la partizione.  
  
     **Gruppo di misure**  
     Consente di visualizzare il nome del gruppo di misure del cubo contenente la partizione.  
  
     **Nome partizione**  
     Consente di visualizzare il nome della partizione.  
  
     **Dimensioni (MB)**  
     Consente di visualizzare le dimensioni in megabyte della partizione.  
  
6.  Specificare se includere le informazioni sulle autorizzazioni utente e se utilizzare la compressione. Per impostazione predefinita, la procedura guidata comprime tutti i dati e i metadati prima di copiare i file nel server di destinazione. Questa opzione comporta una trasmissione di file più rapida. I file vengono decompressi dopo aver raggiunto il server di destinazione.  
  
     **Copia tutto**  
     Selezionare questa opzione per includere definizioni di sicurezza e informazioni sull'appartenenza durante la sincronizzazione.  
  
     **Ignora appartenenza**  
     Selezionare questa opzione per includere le definizioni di sicurezza ma non le informazioni sull'appartenenza durante la sincronizzazione.  
  
     **Ignora tutto**  
     Selezionare questa opzione per ignorare la definizione di sicurezza e le informazioni sull'appartenenza attualmente incluse nel database di origine. Se un database di destinazione viene creato durante la sincronizzazione, non verranno copiate le definizioni di sicurezza né le informazioni sull'appartenenza. Se il database di destinazione esiste già e contiene i ruoli e le appartenenze, tali informazioni di sicurezza verranno mantenute.  
  
7.  Scegliere il metodo di sincronizzazione. È possibile eseguire immediatamente la sincronizzazione o generare uno script che verrà salvato in un file. Per impostazione predefinita, il file viene salvato con estensione XMLA e posizionato nella cartella Documenti.  
  
8.  Fare clic su **Fine** per eseguire la sincronizzazione. Dopo aver verificato le opzioni nella pagina **Completamento procedura guidata** fare di nuovo clic su **Fine** .  
  
## <a name="next-steps"></a>Passaggi successivi  
 Se non viene eseguita la sincronizzazione di ruoli o appartenenze, ricordarsi di specificare ora le autorizzazioni di accesso utente nel database di destinazione.  
  
## <a name="see-also"></a>Vedi anche  
 [Elemento Synchronize &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Distribuire soluzioni di modelli tramite XMLA](deploy-model-solutions-using-xmla.md)   
 [Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
