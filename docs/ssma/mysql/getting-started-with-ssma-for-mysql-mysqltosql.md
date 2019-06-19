---
title: Introduzione a SSMA per MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1ae91f90bf601e4ef17ae2f363260dbb47a2822e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187141"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Introduzione a SSMA per MySQL (MySQLToSQL)
SQL Server Migration Assistant (SSMA) per MySQL consente di convertire gli schemi di database MySQL in schemi di SQL Server o database SQL di Azure, caricare gli schemi risultanti in SQL Server o database SQL di Azure e la migrazione dei dati da MySQL a SQL Server o database SQL di Azure.  
  
Questo argomento illustra il processo di installazione e quindi consente di acquisire familiarità con l'interfaccia utente SSMA.  
  
## <a name="installing-ssma"></a>Installazione di SSMA  
Per usare SSMA, è necessario installare il programma client SSMA su un computer in cui è possibile accedere al database MySQL di origine e l'istanza di destinazione di SQL Server o database SQL di Azure. Quindi, installare i provider di MySQL (Driver ODBC MySQL 5.1 (attendibili)) nel computer che esegue il programma Client di SSMA. Per istruzioni sull'installazione, vedere [installazione di SSMA per MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Per avviare SSMA, fare clic su **avviare**, scegliere **tutti i programmi**, scegliere **SQL Server Migration Assistant per MySQL**, quindi fare clic su **migrazione a SQL Server Assistant per MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA per l'interfaccia utente di MySQL  
Dopo aver SSMA viene installato e concesso in licenza, è possibile utilizzare SSMA per la migrazione di database MySQL a SQL Server o database SQL di Azure. Consente di acquisire familiarità con l'interfaccia utente SSMA prima di iniziare. Il diagramma seguente mostra l'interfaccia utente per SSMA, tra cui le finestre di esplorazione di metadati, metadati, le barre degli strumenti, riquadro di output e riquadro elenco errori:  
  
![SSMA per l'interfaccia utente grafica MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA per l'interfaccia utente grafica MySql")  
  
Per avviare una migrazione, è necessario:  
  
1.  Creare un nuovo progetto.  
  
2.  Connettersi a un database MySQL.  
  
3.  Dopo la connessione ha esito positivo, gli schemi di MySQL verranno visualizzato nel Visualizzatore metadati MySQL. Oggetti pulsante destro del mouse nel Visualizzatore metadati di MySQL per eseguire attività quali la creano di report che valutano le conversioni in SQL Server/Azure SQL DB.  
  
È anche possibile eseguire queste attività usando le barre degli strumenti e i menu.  
  
È anche necessario connettersi a un'istanza di SQL Server. Dopo la connessione ha esito positivo, verrà visualizzata una gerarchia di database di SQL Server in Esplora i metadati di SQL Server. Dopo la conversione degli schemi di MySQL in schemi di SQL Server, selezionare tali schemi convertiti nel Visualizzatore metadati di SQL Server e quindi sincronizzare gli schemi con SQL Server.  
  
Se si è scelto un database SQL di Azure dalla migrazione di elenco a discesa nella finestra di dialogo Nuovo progetto, è necessario connettersi al database SQL di Azure. Dopo la connessione ha esito positivo, verrà visualizzata una gerarchia di database di Azure SQL DB in Azure SQL DB metadati Explorer. Dopo la conversione degli schemi di MySQL in schemi di database SQL di Azure, selezionare tali schemi convertiti nel Visualizzatore metadati di Azure SQL DB e quindi sincronizzare gli schemi con database SQL di Azure.  
  
Dopo aver sincronizzato gli schemi convertiti con SQL Server o database SQL di Azure, è possibile tornare a Visualizzatore metadati MySQL e migrare i dati da schemi di MySQL in database di SQL Server o database SQL di Azure.  
  
Per altre informazioni su queste attività e su come eseguirle, vedere [migrazione di database MySQL a SQL Server - database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
Le sezioni seguenti descrivono le funzionalità dell'interfaccia utente di SSMA.  
  
### <a name="metadata-explorers"></a>Strumenti di esplorazione di metadati  
SSMA contiene due finestre di esplorazione di metadati per individuare ed eseguire azioni sul database MySQL e SQL Server.  
  
### <a name="mysql-metadata-explorer"></a>Visualizzatore metadati MySQL  
Visualizzatore metadati MySQL Mostra informazioni sugli schemi di MySQL. Tramite Visualizzatore metadati MySQL, è possibile eseguire le attività seguenti:  
  
-   Esplorare gli oggetti in ogni schema.  
  
-   Selezionare gli oggetti per la conversione e quindi convertire gli oggetti di sintassi di SQL Server. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Selezionare le tabelle per la migrazione dei dati e quindi migrare i dati da tali tabelle in SQL Server. Per altre informazioni, vedere [eseguire la migrazione di dati di MySQL in SQL Server - database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>Visualizzatore metadati di database SQL di Azure o SQL Server  
SQL Server o Azure SQL DB metadati Explorer mostra le informazioni relative a un'istanza di SQL Server o database SQL di Azure. Quando ci si connette a un'istanza di SQL Server o database SQL di Azure, SSMA recupera i metadati relativi a tale istanza e la archivia nel file di progetto.  
  
È possibile utilizzare questa finestra di esplorazione di metadati per selezionare gli oggetti di database convertiti MySQL e quindi sincronizzare gli oggetti con l'istanza di SQL Server o database SQL di Azure.  
  
Per altre informazioni, vedere [sincronizzazione (MySQL a SQL Server / database SQL di Azure)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadati  
A destra di ogni Visualizzatore metadati sono schede che descrivono l'oggetto selezionato. Ad esempio, se si seleziona una tabella nel Visualizzatore metadati MySQL, verranno visualizzate nove schede: **Nella tabella**, **SQL**, **Mapping dei tipi**, **dati**, **impostazioni**, **Mapping di set di caratteri**, **Modalità SQL**, **delle proprietà**, e **Report**. Il **Report** scheda contiene informazioni solo dopo aver creato un report che contiene l'oggetto selezionato. Se si seleziona una tabella in Esplora i metadati di SQL Server, verranno visualizzate tre schede: **Nella tabella**, **SQL** e **dati**.  
  
La maggior parte delle impostazioni dei metadati sono di sola lettura. Tuttavia, è possibile modificare i metadati seguenti:  
  
-   Nel Visualizzatore metadati di MySQL, è possibile modificare i mapping dei tipi, Mapping di set di caratteri, le modalità di SQL. Per convertire il mapping dei tipi modificata o il Mapping di set di caratteri o modalità SQL, apportare modifiche prima di convertire gli schemi.  
  
-   In Esplora i metadati di SQL Server, è possibile modificare le proprietà di tabella e indice nella scheda della tabella. Per visualizzare queste modifiche in SQL Server, apportare queste modifiche prima di caricare gli schemi in SQL Server.  
  
Le modifiche apportate in una finestra di esplorazione di metadati vengono riflesse nei metadati del progetto, non nel database di origine o destinazione.  
  
### <a name="toolbars"></a>Barre degli strumenti  
SSMA è due barre degli strumenti: una barra di progetto e una barra degli strumenti di migrazione.  
  
### <a name="the-project-toolbar"></a>La barra degli strumenti di progetto  
La barra degli strumenti di progetto contiene pulsanti per l'uso dei progetti, la connessione a MySQL e ci si connette a SQL Server o database SQL di Azure. Questi pulsanti sono simili a quelli nel **File** menu.  
  
### <a name="migration-toolbar"></a>Sulla barra degli strumenti di migrazione  
La tabella seguente illustra la migrazione i comandi della barra degli strumenti:  
  
|||  
|-|-|  
|**Pulsante**|**Funzione**|  
|**Creazione di Report**|Converte gli oggetti selezionati di MySQL per gli oggetti di SQL Server o database SQL di Azure e quindi crea un report che mostra la conversione ha come esito positivo.<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati MySQL.|  
|**Converti Schema**|Converte gli oggetti selezionati di MySQL in oggetti di SQL Server o database SQL di Azure.<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati MySQL.|  
|**La migrazione dei dati**|Esegue la migrazione di dati dal database MySQL a SQL Server o database SQL di Azure. Prima di eseguire questo comando, è necessario convertire gli schemi di MySQL in schemi di SQL Server o database SQL di Azure e quindi caricare gli oggetti in SQL Server o database SQL di Azure.<br /><br />Questo comando è disabilitato, a meno che gli oggetti selezionati in Visualizzatore metadati MySQL.|  
|**Arresta**|Arresta il processo corrente.|  
  
### <a name="menus"></a>Menu  
La tabella seguente mostra i menu SSMA.  
  
|||  
|-|-|  
|**Menu**|**Descrizione**|  
|**File**|Contiene i comandi per l'utilizzo con i progetti, la connessione a MySQL e ci si connette a SQL Server o database SQL di Azure.|  
|**Modifica**|Contiene i comandi per la ricerca e lavora sul testo nelle pagine di dettagli. Per aprire **gestire i segnalibri** finestra di dialogo, dal menu Modifica fare clic su Gestisci segnalibri. Nella finestra di dialogo verrà visualizzato un elenco dei propri segnalibri esistenti. È possibile usare i pulsanti sul lato destro della finestra di dialogo per gestire i segnalibri.|  
|**Visualizza**|Contiene il **strumenti di esplorazione di sincronizzare i metadati** comando. Che consente di sincronizzare gli oggetti tra Visualizzatore metadati MySQL e SQL Server o Azure SQL DB metadati Explorer. Contiene anche i comandi per mostrare e nascondere il **Output** e **elenco errori** riquadri e un'opzione **layout** per gestire il layout.|  
|**Strumenti**|Contiene i comandi per creare report, convertire lo schema, aggiornare dal database, eseguire la migrazione di oggetti e dati e salvare come Script. Fornisce inoltre l'accesso per il **impostazioni globali, le impostazioni di progetto predefinito** e **le impostazioni del progetto** finestre di dialogo.|  
|**?**|Fornisce l'accesso per SSMA e di ottenere il **sulle** nella finestra di dialogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Riquadro di output e il riquadro elenco errori  
Il **vista** menu sono disponibili comandi per attivare o disattivare la visibilità del riquadro di Output e il riquadro elenco errori:  
  
-   Il riquadro di Output Mostra i messaggi di stato da SSMA durante la conversione degli oggetti di sincronizzazione dell'oggetto e migrazione dei dati.  
  
-   Nel riquadro elenco errori Mostra messaggi di errore, avviso e informativi in un elenco ordinabile.  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'interfaccia utente &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[La migrazione dei dati di MySQL in - database SQL di Azure SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
