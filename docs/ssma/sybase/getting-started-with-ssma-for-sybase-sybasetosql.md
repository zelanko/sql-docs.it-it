---
title: Introduzione a SSMA per SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f07f230f52fee5707084c01060e92220b35cb75c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029119"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Introduzione a SSMA per SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per SAP ASE consente rapidamente gli schemi di database SAP Adaptive Server Enterprise (ASE) per convertire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli schemi di Database SQL di Azure, caricare gli schemi risultanti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure ed eseguire la migrazione dei dati da SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.  
  
Questo argomento illustra il processo di installazione e quindi consente di acquisire familiarità con l'interfaccia utente SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Installazione e la gestione delle licenze di SSMA  
Per usare SSMA, è innanzitutto necessario installare il programma client SSMA in un computer che può accedere sia l'istanza di origine di SAP ASE e l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Per usare la migrazione dei dati lato server, è necessario installare il pacchetto di estensione e almeno uno dei provider di SAP ASE (OLE DB o ADO.NET) nel computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi componenti supportano la migrazione dei dati e l'emulazione delle funzioni di sistema di SAP ASE. Per istruzioni sull'installazione, vedere [installazione di SSMA per ASE SAP &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Per avviare SSMA, fare clic su **avviare**, scegliere **tutti i programmi**, scegliere  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Sybase**e quindi scegliere  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Sybase**. La prima volta che si avvia SSMA, viene visualizzata una finestra di dialogo Gestione delle licenze. È necessario ottenere una licenza SSMA utilizzando un Windows Live ID prima di poter usare SSMA. Le istruzioni di gestione delle licenze sono incluse con le istruzioni di installazione nel [installazione di SSMA per Sybase Client &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) argomento.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA per l'interfaccia utente di SAP ASE  
Dopo aver SSMA viene installato e concesso in licenza, è possibile usare SSMA per la migrazione dei database SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Consente di acquisire familiarità con l'interfaccia utente SSMA prima di iniziare. Il diagramma seguente mostra l'interfaccia utente per SSMA, tra cui le finestre di esplorazione di metadati, metadati, le barre degli strumenti, riquadro di output e riquadro elenco errori:  
  
![SSMA per l'interfaccia utente di ambiente del servizio app di SAP](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA per l'interfaccia utente di ASE SAP")  
  
Per avviare una migrazione, è innanzitutto necessario creare un nuovo progetto. Quindi, è connettersi a SAP ASE. Dopo la connessione ha esito positivo, verrà visualizzata una gerarchia di database SAP ASE in Visualizzatore metadati Sybase. È possibile quindi oggetti pulsante destro del mouse nel Visualizzatore metadati Sybase per eseguire le attività, ad esempio creano i report che valutano le conversioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. È anche possibile eseguire queste attività tramite il menu e barre degli strumenti.  
  
È anche necessario connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Dopo la connessione ha esito positivo, una gerarchia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o i database SQL di Azure verranno visualizzati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure. Dopo la conversione di schemi SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli schemi di Database SQL di Azure, selezionare tali schemi convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure e quindi caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.  
  
Dopo il caricamento degli schemi convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure il Database SQL di Azure, è possibile tornare a Visualizzatore metadati Sybase e migrare i dati da database di SAP ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
Per altre informazioni su queste attività e su come eseguirle, vedere [eseguire la migrazione di database SAP ASE a SQL Server - Database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
Le sezioni seguenti descrivono le funzionalità dell'interfaccia utente di SSMA.  
  
### <a name="metadata-explorers"></a>Strumenti di esplorazione di metadati  
SSMA contiene due finestre di esplorazione di metadati per individuare ed eseguire azioni su SAP ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
#### <a name="sybase-metadata-explorer"></a>Visualizzatore metadati Sybase  
Visualizzatore metadati Sybase illustra informazioni sui database nell'istanza di origine di SAP ASE.  
  
Tramite Visualizzatore metadati Sybase, è possibile eseguire le attività seguenti:  
  
-   Esplorare le tabelle in ogni database.  
  
-   Selezionare gli oggetti per la conversione e quindi convertire gli oggetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di Database SQL di Azure. Per altre informazioni, vedere [convertire gli oggetti di Database di SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Selezionare gli oggetti per la migrazione dei dati e quindi migrare i dati da tali oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Per altre informazioni, vedere [eseguire la migrazione di dati SAP ASE in SQL Server - Database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>Visualizzatore metadati di SQL Azure o SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure Mostra informazioni su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure, SSMA recupera i metadati relativi a tale istanza e lo archivia nel file di progetto.  
  
È possibile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati di SQL Azure per selezionare gli oggetti di database SAP ASE convertiti e quindi caricare o (sincronizzazione) gli oggetti nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.  
  
Per altre informazioni, vedere [caricamento di convertire gli oggetti di Database in SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadata  
A destra di ogni Visualizzatore metadati sono schede che descrivono l'oggetto selezionato. Ad esempio, se si seleziona una tabella nel Visualizzatore metadati Sybase, vengono visualizzati sei schede: **Nella tabella**, **SQL**, **Mapping dei tipi**, **dati**, **proprietà**, e **Report**. Il **Report** scheda contiene informazioni solo dopo aver creato un report che contiene l'oggetto selezionato. Se si seleziona una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure, visualizzata come tre schede: **Nella tabella**, **SQL**, e **dati**.  
  
La maggior parte delle impostazioni dei metadati sono di sola lettura. Tuttavia, è possibile modificare i metadati seguenti:  
  
-   Nel Visualizzatore metadati Sybase, è possibile alter procedure e i mapping dei tipi. Apportare queste modifiche prima di convertire gli schemi.  
  
-   Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure Esplora i metadati di SQL Azure, è possibile modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] per le stored procedure. Apportare queste modifiche prima di caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Le modifiche apportate in una finestra di esplorazione di metadati vengono riflesse nei metadati del progetto, non nel database di origine o destinazione.  
  
### <a name="toolbars"></a>Barre degli strumenti  
SSMA è due barre degli strumenti: una barra di progetto e una barra degli strumenti di migrazione.  
  
#### <a name="the-project-toolbar"></a>La barra degli strumenti di progetto  
Progetto contenente pulsanti per l'utilizzo con i progetti, la connessione a SAP ASE e ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Questi pulsanti sono simili a quelli nel **File** menu.  
  
#### <a name="the-migration-toolbar"></a>Barra degli strumenti di migrazione  
Barra degli strumenti di migrazione include i comandi seguenti:  
  
|Button|Funzione|  
|----------|------------|  
|**Creazione di Report**|Converte gli oggetti selezionati SAP ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi e quindi crea un report che mostra la conversione ha come esito positivo.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati Sybase.|  
|**Converti Schema**|Converte gli oggetti selezionati SAP ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di Database SQL di Azure.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati Sybase.|  
|**La migrazione dei dati**|Esegue la migrazione di dati dal database di SAP ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure. Prima di eseguire questo comando, è necessario convertire gli schemi di SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli schemi di Database SQL di Azure e quindi caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati Sybase.|  
|**Arresta**|Arresta il processo corrente, ad esempio la conversione di oggetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di Database SQL di Azure.|  
  
### <a name="menus"></a>Menu  
SSMA contiene i menu seguenti:  
  
|Menu|Descrizione|  
|--------|---------------|  
|**File**|Comandi per l'uso dei progetti, la connessione a SAP ASE e ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Database SQL di Azure.|  
|**Modifica**|Contiene i comandi per la ricerca e lavora sul testo nelle pagine di dettagli, ad esempio la copia [!INCLUDE[tsql](../../includes/tsql-md.md)] dal riquadro dei dettagli SQL. Contiene anche il **gestire i segnalibri** opzione, in cui è possibile visualizzare un elenco dei propri segnalibri esistenti. È possibile usare i pulsanti sul lato destro della finestra di dialogo per gestire i segnalibri.|  
|**Visualizza**|Contiene il **strumenti di esplorazione di sincronizzare i metadati** comando. Ciò consente di sincronizzare gli oggetti tra Visualizzatore metadati Sybase e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure. Contiene anche i comandi per visualizzare e nascondere il **Output** e **elenco errori** riquadri e un'opzione **layout** per gestire i layout.|  
|**Strumenti**|Contiene i comandi per creare report, esportare i dati e la migrazione di oggetti e dati. Fornisce inoltre l'accesso per il **impostazioni globali** e **le impostazioni del progetto** finestre di dialogo.|  
|**Tester**|Contiene i comandi per creare test case, visualizzare i risultati di test e i comandi per la gestione di backup di database.|  
|**?**|Fornisce l'accesso per SSMA e di ottenere il **sulle** nella finestra di dialogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Riquadro di output e il riquadro elenco errori  
Il **vista** menu sono disponibili comandi per attivare o disattivare la visibilità del riquadro di Output e il riquadro elenco errori:  
  
-   Il riquadro di Output Mostra i messaggi di stato da SSMA durante la conversione degli oggetti di sincronizzazione dell'oggetto e migrazione dei dati.  
  
-   Nel riquadro elenco errori Mostra messaggi di errore, avviso e informativi in un elenco che è possibile ordinare.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di database SAP ASE a SQL Server - Database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Riferimento all'interfaccia utente &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
