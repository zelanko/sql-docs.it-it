---
title: Introduzione a SSMA per Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 80fc86c4b3d9385dc056b0c0ea9633f9f5f26675
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68220599"
---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>Introduzione a SSMA per Oracle (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per Oracle consente rapidamente gli schemi di database Oracle per convertire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi, caricare gli schemi risultanti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ed eseguire la migrazione dei dati da Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Questo argomento illustra il processo di installazione e quindi consente di acquisire familiarità con l'interfaccia utente SSMA.  
  
## <a name="installing-ssma"></a>Installazione di SSMA  
Per usare SSMA, è innanzitutto necessario installare il programma client SSMA in un computer che può accedere al database Oracle di origine sia l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È quindi necessario installare un pacchetto di estensione e almeno uno dei provider Oracle (OLE DB o [!INCLUDE[vstecado](../../includes/vstecado_md.md)]) nel computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi componenti supportano la migrazione dei dati e l'emulazione delle funzioni di sistema Oracle. Per istruzioni sull'installazione, vedere [installazione di SSMA per Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md).  
  
Per avviare SSMA, fare clic su **avviare**, scegliere **tutti i programmi**, scegliere  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant per Oracle**, quindi fare clic su  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant per Oracle**.  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA per Oracle l'interfaccia utente  
Dopo aver installato SSMA, è possibile usare SSMA per la migrazione di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Consente di acquisire familiarità con l'interfaccia utente SSMA prima di iniziare. Il diagramma seguente mostra l'interfaccia utente per SSMA, tra cui le finestre di esplorazione di metadati, metadati, le barre degli strumenti, riquadro di output e riquadro elenco errori:  
  
![SSMA per l'interfaccia utente di Oracle](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA per Oracle dell'interfaccia utente")  
  
Per avviare una migrazione, è innanzitutto necessario creare un nuovo progetto. Quindi, connettersi a un database Oracle. Dopo la connessione ha esito positivo, gli schemi Oracle verranno visualizzati nel Visualizzatore metadati Oracle. È possibile quindi oggetti pulsante destro del mouse nel Visualizzatore metadati Oracle per eseguire attività quali la creano di report che valutano le conversioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È anche possibile eseguire queste attività usando le barre degli strumenti e i menu.  
  
È anche necessario connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dopo la connessione ha esito positivo, una gerarchia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database verranno visualizzati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. Dopo la conversione di schemi Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi, selezionare tali schemi convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati e quindi sincronizzare gli schemi con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Dopo aver sincronizzato gli schemi convertiti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile tornare a Visualizzatore metadati Oracle e migrare i dati da schemi Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database.  
  
Per altre informazioni su queste attività e su come eseguirle, vedere [migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md).  
  
Le sezioni seguenti descrivono le funzionalità dell'interfaccia utente di SSMA.  
  
### <a name="metadata-explorers"></a>Strumenti di esplorazione di metadati  
SSMA contiene due finestre di esplorazione di metadati per individuare ed eseguire azioni in Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
#### <a name="oracle-metadata-explorer"></a>Visualizzatore metadati Oracle  
Visualizzatore metadati Oracle Mostra informazioni sugli schemi Oracle. Tramite Visualizzatore metadati Oracle, è possibile eseguire le attività seguenti:  
  
-   Esplorare gli oggetti in ogni schema.  
  
-   Selezionare gli oggetti per la conversione e quindi convertire gli oggetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi. Per altre informazioni, vedere [conversione di schemi Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
-   Selezionare le tabelle per la migrazione dei dati e quindi migrare i dati da tali tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [eseguire la migrazione di dati Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Esplora i metadati SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati Mostra le informazioni su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA recupera i metadati relativi a tale istanza e lo archivia nel file di progetto.  
  
È possibile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati per selezionare gli oggetti di database convertiti Oracle e quindi sincronizzare gli oggetti con l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Per altre informazioni, vedere [caricamento di convertire gli oggetti di Database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
### <a name="metadata"></a>Metadata  
A destra di ogni Visualizzatore metadati sono schede che descrivono l'oggetto selezionato. Ad esempio, se si seleziona una tabella nel Visualizzatore metadati Oracle, verranno visualizzate sei schede: **Nella tabella**, **SQL**, **digitare Mapping, Report**, **proprietà**, e **dati**. Il **Report** scheda contiene informazioni solo dopo aver creato un report che contiene l'oggetto selezionato. Se si seleziona una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, verranno visualizzate tre schede: **Nella tabella**, **SQL**, e **dati**.  
  
La maggior parte delle impostazioni dei metadati sono di sola lettura. Tuttavia, è possibile modificare i metadati seguenti:  
  
-   Nel Visualizzatore metadati Oracle, è possibile alter procedure e i mapping dei tipi. Per convertire le procedure modificate e i mapping dei tipi, apportare modifiche prima di convertire gli schemi.  
  
-   Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, è possibile modificare il [!INCLUDE[tsql](../../includes/tsql-md.md)] per le stored procedure. Per visualizzare queste modifiche nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], apportare queste modifiche prima di caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Le modifiche apportate in una finestra di esplorazione di metadati vengono riflesse nei metadati del progetto, non nel database di origine o destinazione.  
  
### <a name="toolbars"></a>Barre degli strumenti  
SSMA è due barre degli strumenti: una barra di progetto e una barra degli strumenti di migrazione.  
  
#### <a name="the-project-toolbar"></a>La barra degli strumenti di progetto  
Progetto contenente pulsanti per l'utilizzo con i progetti, la connessione a Oracle e la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi pulsanti sono simili a quelli nel **File** menu.  
  
#### <a name="migration-toolbar"></a>Sulla barra degli strumenti di migrazione  
La tabella seguente illustra la migrazione i comandi della barra degli strumenti:  
  
|Button|Funzione|  
|------|--------|  
|**Creazione di Report**|Converte gli oggetti selezionati di Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi e quindi crea un report che mostra la conversione ha come esito positivo.<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati Oracle.|  
|**Converti Schema**|Converte gli oggetti selezionati di Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti.<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati Oracle.|  
|**La migrazione dei dati**|Esegue la migrazione di dati dal database di Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Prima di eseguire questo comando, è necessario convertire gli schemi di Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi, quindi caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati Oracle.|  
|**Arresta**|Arresta il processo corrente.|  
  
### <a name="menus"></a>Menu  
La tabella seguente mostra i menu SSMA.  
  
|Menu|Descrizione|  
|----|-----------|  
|**File**|Comandi per l'uso dei progetti, la connessione a Oracle e la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Modifica**|Contiene i comandi per la ricerca e lavora sul testo nelle pagine di dettagli, ad esempio la copia [!INCLUDE[tsql](../../includes/tsql-md.md)] dal riquadro dei dettagli SQL. Contiene anche il **gestire i segnalibri** opzione, in cui sarà in grado di visualizzare un elenco dei propri segnalibri esistenti. È possibile usare i pulsanti sul lato destro della finestra di dialogo per gestire i segnalibri.|  
|**Visualizza**|Contiene il **strumenti di esplorazione di sincronizzare i metadati** comando. Che consente di sincronizzare gli oggetti tra Visualizzatore metadati Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. Contiene anche i comandi per mostrare e nascondere il **Output** e **elenco errori** riquadri e un'opzione **layout** per gestire i layout.|  
|**Strumenti**|Contiene i comandi per creare report ed eseguire la migrazione di oggetti e dati. Fornisce inoltre l'accesso per il **impostazioni globali** e **le impostazioni del progetto** finestre di dialogo.|  
|**Tester**|Contiene i comandi per la creazione e utilizzo di test case, il repository e del sistema di gestione di backup.|  
|**?**|Fornisce l'accesso per SSMA e di ottenere il **sulle** nella finestra di dialogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Riquadro di output e il riquadro elenco errori  
Il **vista** menu sono disponibili comandi per attivare o disattivare la visibilità del riquadro di Output e il riquadro elenco errori:  
  
-   Il riquadro di output mostra i messaggi di stato da SSMA durante la conversione degli oggetti di sincronizzazione dell'oggetto e migrazione dei dati.  
  
-   Nel riquadro elenco errori Mostra messaggi di errore, avviso e informativi in un elenco ordinabile.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione di dati Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[Riferimento all'interfaccia utente &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
