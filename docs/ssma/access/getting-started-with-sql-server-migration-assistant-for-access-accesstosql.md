---
title: Introduzione a SQL Server Migration Assistant per Access | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 863e62dc9e2970f7531bba15f7242c73c5b0f9e7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259918"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introduzione a SQL Server Migration Assistant per Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per l'accesso consente di convertire rapidamente oggetti di database di Access da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di database SQL di Azure, caricare gli oggetti risultanti nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure ed eseguire la migrazione dei dati da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Se necessario, è anche possibile collegare le tabelle di accesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di database SQL di Azure in modo che è possibile continuare a usare le applicazioni front-end Access esistenti con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
Questo argomento illustra il processo di installazione e consente di acquisire familiarità con l'interfaccia utente SSMA.  
  
## <a name="installing-ssma"></a>Installazione di SSMA  
Per usare SSMA, è innanzitutto necessario installare il programma client SSMA su un computer in cui può accedere a entrambi i database che si vuole eseguire la migrazione e l'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Per istruzioni sull'installazione, vedere [installazione di SQL Server Migration Assistant per Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Per avviare SSMA, fare clic su **avviare**, scegliere **tutti i programmi**, scegliere **SQL Server Migration Assistant per Access**e quindi selezionare **migrazione a SQL Server Assistente per l'accesso**.  
  
## <a name="using-ssma"></a>Uso di SSMA  
Dopo l'installazione di SSMA, è utile per acquisire familiarità con l'interfaccia utente SSMA prima di usare lo strumento per eseguire la migrazione di database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. L'interfaccia utente SSMA, tra cui le finestre di esplorazione di metadati, metadati, le barre degli strumenti, riquadro di output e riquadro elenco errori vengono visualizzati nel diagramma seguente:  
  
![SSMA per l'interfaccia utente grafica di Access](../../ssma/access/media/ssmaforaccessgui.gif "SSMA per l'interfaccia utente grafica di accesso")  
  
Per avviare una migrazione, creare un nuovo progetto e quindi aggiungere i database di Access a Visualizzatore metadati di accesso. È quindi possibile fare doppio clic sugli oggetti in Esplora i metadati di accesso per eseguire attività quali:
- Esportazione di un inventario degli oggetti di database di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.
- Creazione di report che valutano le conversioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.
- Conversione di schemi di accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o degli schemi di database SQL di Azure.

È anche possibile eseguire queste attività usando le barre degli strumenti e i menu.  
  
È anche necessario connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dopo la connessione ha esito positivo, una gerarchia di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database viene visualizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati. Dopo la conversione degli schemi di accesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi, è possibile selezionare tali schemi convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati e quindi caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se si è scelto il database SQL di Azure dalla migrazione di elenco a discesa nella finestra di dialogo Nuovo progetto, è necessario connettersi al database SQL di Azure. Dopo la connessione ha esito positivo, viene visualizzata una gerarchia di database di Azure SQL DB in Azure SQL DB metadati Esplora. Dopo la conversione degli schemi di accesso agli schemi di database SQL di Azure, è possibile selezionare tali schemi convertiti nel Visualizzatore metadati di Azure SQL DB e quindi caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Dopo il caricamento degli schemi convertiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il database SQL di Azure, è possibile tornare a Visualizzatore metadati di accesso e la migrazione dei dati dal database di Access in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o i database di database SQL di Azure. Se necessario, è anche possibile collegare le tabelle di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di database SQL di Azure.  
  
Per altre informazioni su queste attività e su come eseguirle, vedere gli argomenti seguenti:  
  
-   [Preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [Collegamento delle applicazioni di accesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
Le sezioni seguenti descrivono le funzionalità dell'interfaccia utente di SSMA.  
  
### <a name="metadata-explorers"></a>Strumenti di esplorazione di metadati  
SSMA contiene due finestre di esplorazione dei metadati che è possibile usare per esplorare ed eseguire azioni su accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o i database di database SQL di Azure.  
  
#### <a name="access-metadata-explorer"></a>Accedi a Visualizzatore metadati  
Visualizzatore metadati accesso illustra informazioni sui database di Access che sono stati aggiunti al progetto. Quando si aggiunge un database di Access, SSMA recupera i metadati relativi a quel database, ovvero i metadati che sono disponibili nel Visualizzatore metadati di accesso.  
  
È possibile usare Visualizzatore metadati di accesso per eseguire le attività seguenti:  
  
-   Esplorare le tabelle in ogni database di Access.  
  
-   Selezionare gli oggetti per la conversione e convertire gli oggetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi. Per altre informazioni, vedere [conversione di oggetti di Database di Access](converting-access-database-objects-accesstosql.md).  
  
-   Selezionare gli oggetti per la migrazione dei dati e la migrazione dei dati da tali oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [la migrazione di accesso ai dati in SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
-   Collegare e scollegare l'accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>Visualizzatore metadati di database SQL di Azure o SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB metadati Explorer mostra le informazioni su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure, SSMA recupera i metadati relativi a tale istanza e lo archivia nel file di progetto.  
  
È possibile usare il Server SQL o Azure SQL DB metadati Explorer per selezionare gli oggetti di database convertiti accesso e caricare (sincronizzazione) gli oggetti nell'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.  
  
Per altre informazioni, vedere [caricamento di convertire gli oggetti di Database in SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
### <a name="metadata"></a>Metadata  
A destra di ogni Visualizzatore metadati sono schede che descrivono l'oggetto selezionato. Ad esempio, se si seleziona una tabella nel Visualizzatore metadati di accesso, vengono visualizzati quattro schede: **Nella tabella**, **Mapping dei tipi**, **delle proprietà**, e **dati**. Se si seleziona una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, visualizzati tre schede: **Nella tabella**, **SQL**, e **dati**.  
  
La maggior parte delle impostazioni dei metadati sono di sola lettura. Tuttavia, è possibile modificare i metadati seguenti:  
  
-   Nel Visualizzatore metadati di accesso, è possibile modificare i mapping dei tipi. Assicurarsi di apportare queste modifiche prima di creare report o convertire gli schemi.  
  
-   Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Visualizzatore metadati, è possibile modificare le proprietà di tabelle e indici sul **tabella** scheda. Apportare queste modifiche prima di caricare gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [conversione di oggetti di Database di Access](converting-access-database-objects-accesstosql.md).  
  
### <a name="toolbars"></a>Barre degli strumenti  
SSMA è due barre degli strumenti: una barra di progetto e una barra degli strumenti di migrazione.  
  
#### <a name="the-project-toolbar"></a>La barra degli strumenti di progetto  
Progetto contenente pulsanti per l'utilizzo con i progetti, aggiunta di file di database di Access e ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Questi pulsanti sono simili a quelli nel **File** menu.  
  
#### <a name="the-migration-toolbar"></a>Barra degli strumenti di migrazione  
Barra degli strumenti di migrazione include i comandi seguenti:  
  
|Button|Funzione|  
|----------|------------|  
|**Convertire, caricare ed eseguire la migrazione**|Converte i database di Access, carica gli oggetti convertiti nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure e viene eseguita la migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure, tutto in un unico passaggio.|  
|**Creazione di Report**|Converte lo schema selezionato l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di database SQL di Azure e quindi crea un report che mostra la conversione ha come esito positivo.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati di accesso.|  
|**Converti Schema**|Converte lo schema selezionato l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o degli schemi di database SQL di Azure.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati di accesso.|  
|**La migrazione dei dati**|Esegue la migrazione di dati dal database di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Prima di eseguire questo comando, è necessario convertire gli schemi di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli schemi di database SQL di Azure e quindi caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.<br /><br />Questo comando è disponibile solo quando gli oggetti selezionati in Visualizzatore metadati di accesso.|  
|**Arresta**|Arresta il processo corrente, ad esempio la conversione di oggetti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di database SQL di Azure.|  
  
### <a name="menus"></a>Menu  
SSMA contiene i menu seguenti:  
  
|Menu|Descrizione|  
|--------|---------------|  
|**File**|Contiene i comandi per la migrazione guidata, si lavora su progetti, aggiunta e rimozione dei file di database di Access e ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure.|  
|**Modifica**|Contiene i comandi per la ricerca e lavora sul testo nelle pagine di dettagli, ad esempio la copia [!INCLUDE[tsql](../../includes/tsql-md.md)] dal riquadro dei dettagli SQL. Per aprire la **gestire i segnalibri** finestra di dialogo, dal menu Modifica, fare clic su Gestisci segnalibri. Nella finestra di dialogo, verrà visualizzato un elenco dei propri segnalibri esistenti. È possibile usare i pulsanti sul lato destro della finestra di dialogo per gestire i segnalibri.|  
|**Visualizza**|Contiene il **strumenti di esplorazione di sincronizzare i metadati** comando. Ciò consente di sincronizzare gli oggetti tra Visualizzatore metadati di accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di Azure SQL DB. Contiene anche i comandi per visualizzare e nascondere il **Output** e **elenco errori** riquadri e un'opzione **layout** per gestire il layout.|  
|**Strumenti**|Contiene i comandi per creare report, esportare i dati, eseguire la migrazione di oggetti e dati, collegare le tabelle e consente l'accesso globale e le impostazioni del progetto le finestre di dialogo.|  
|**?**|Fornisce l'accesso per SSMA e di ottenere il **sulle** nella finestra di dialogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Riquadro di output e il riquadro elenco errori  
Il **vista** menu sono disponibili comandi per attivare o disattivare la visibilità del riquadro di Output e il riquadro elenco errori:  
  
-   Il riquadro di Output Mostra i messaggi di stato da SSMA durante la conversione degli oggetti di sincronizzazione dell'oggetto e migrazione dei dati.  
  
-   Nel riquadro elenco errori Mostra messaggi di errore, avviso e informativi in un elenco che è possibile ordinare.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
