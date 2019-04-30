---
title: Uso dei progetti SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 518f899118d5a7d2dce4f56d185fce9d5b1e47df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287844"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Utilizzo dei progetti SSMA (MySQLToSQL)
Per eseguire la migrazione di database MySQL a SQL Server o SQL Azure, è innanzitutto necessario creare un progetto SSMA. Il progetto è un file che contiene le informazioni seguenti:  
  
-   Metadati sui database MySQL che si desidera eseguire la migrazione a SQL Server o SQL Azure.  
  
-   Metadati relativi a questa istanza di destinazione di SQL Server o SQL Azure in cui verranno inseriti gli oggetti migrati e dati.  
  
-   Informazioni di connessione SQL Server o SQL Azure.  
  
-   Impostazioni del progetto.  
  
Quando si apre un progetto, questo viene disconnesso da MySQL e SQL Server o SQL Azure. Che consente di lavorare offline. Per altre informazioni su come connettersi a SQL Server, vedere [connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Esame impostazioni predefinite del progetto  
SSMA contiene diverse impostazioni per la conversione e il caricamento di database, la migrazione dei dati e sincronizzazione SSMA con MySQL e SQL Server o SQL Azure. Le impostazioni predefinite sono appropriate per molti utenti. Tuttavia, prima di creare un nuovo progetto SSMA, è consigliabile verificare le impostazioni. Se necessario, è possibile modificare le impostazioni predefinite che verranno usate per tutti i nuovi progetti.  
  
##### <a name="to-review-default-project-settings"></a>Per controllare le impostazioni di progetto predefinito  
  
1.  Selezionare **impostazioni di progetto predefinite** dalle **strumenti** menu.  
  
2.  Selezionare il tipo di progetto in **versione di destinazione della migrazione** elenco a discesa per quali impostazioni devono essere visualizzati o modificati e quindi fare clic su **generali** scheda.  
  
3.  Nel riquadro sinistro, fare clic su **conversione**.  
  
4.  Nel riquadro di destra, esaminare e modificare le impostazioni in base alle esigenze. Per altre informazioni su queste impostazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Ripetere i passaggi da 1 a 3 per le pagine di migrazione, la sincronizzazione, SQL Azure, interfaccia utente grafica e del mapping dei tipi.  
  
-   Per informazioni sulle impostazioni di migrazione, vedere [impostazioni del progetto &#40;migrazione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Per informazioni sulle impostazioni per la sincronizzazione da SQL Server, vedere [impostazioni del progetto &#40;sincronizzazione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Per informazioni sulle impostazioni di interfaccia utente grafica, vedere [Project. le impostazioni (GUI) (SSMA comuni)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Per informazioni sulle impostazioni di mapping dei tipi di dati, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Per informazioni sulle impostazioni di SQL Azure, vedere [impostazioni del progetto &#40;database SQL di Azure&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> Le impostazioni di SQL Azure verranno visualizzate solo quando si seleziona **migrazione a SQL Azure** durante la creazione di un progetto.  
  
## <a name="creating-new-projects"></a>Creazione di nuovi progetti  
Per eseguire la migrazione dei dati dal database MySQL a SQL Server o SQL Azure, è necessario creare un progetto.  
  
##### <a name="to-create-a-new-project"></a>Per creare un nuovo progetto  
  
1.  Selezionare **nuovo progetto** dalle **File** menu. Verrà visualizzata la finestra di dialogo **Nuovo progetto** . Scegliere **Nuovo progetto** dal menu **File**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nel **nome** immettere un nome per il progetto.  
  
3.  Nel **posizione** casella, immettere o selezionare una cartella per il progetto.  
  
4.  Nel **migrazione a** elenco a discesa, selezionare la versione del server di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato per la migrazione. Le opzioni disponibili sono:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Database SQL di Azure  
  
E quindi fare clic su **OK**  
  
SSMA consente di creare il file di progetto.  
  
## <a name="customizing-project-settings"></a>Personalizzazione delle impostazioni di progetto  
Oltre a definire il valore predefinito delle impostazioni di progetto che si applicano a tutti i nuovi progetti SSMA è inoltre possono personalizzare le impostazioni per ogni progetto. Per altre informazioni, vedere [impostazione delle opzioni progetto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Quando si personalizzano i mapping tra i database di origine e destinazione, è possibile definire i mapping per il progetto, database o a livello di oggetto. Per altre informazioni, vedere [Mapping di MySQL e SQL Server Data Types &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Il salvataggio dei progetti  
La funzionalità di salvataggio progetti consente all'utente essenzialmente salvare le impostazioni del progetto e, facoltativamente, i metadati del database per il file di progetto SSMA.  
  
##### <a name="to-save-a-project"></a>Per salvare un progetto  
  
-   Nel **File** dal menu **salvare** progetto.  
  
Se i database all'interno del progetto sono stati modificati o non sono stati convertiti, SSMA richiederà di caricare e salvare i metadati. Il caricamento e salvataggio dei metadati consente di lavorare offline. Consente inoltre di inviare un file di progetto completo ad altre persone, ad esempio il personale di supporto tecnico. Se viene chiesto di salvare i metadati, eseguire le operazioni seguenti:  
  
1.  Per ogni database che viene visualizzato lo stato **i metadati mancanti**, selezionare la casella di controllo accanto al nome del database. Salvataggio di metadati potrebbe richiedere alcuni minuti. Se non si desidera salvare i metadati a questo punto, non selezionare le caselle di controllo.  
  
2.  Fare clic su **Salva**.  
  
Analizza gli schemi di MySQL e salvare i metadati del file di progetto SSMA.  
  
## <a name="opening-projects"></a>Apertura di progetti  
Quando si apre un progetto, questo viene disconnesso da MySQL e da SQL Server o SQL Azure. Ciò consente di lavorare offline. Per aggiornare i metadati, caricare gli oggetti di database in SQL Server o SQL Azure. Per eseguire la migrazione dei dati, è necessario riconnettersi a SQL Server o SQL Azure.  
  
##### <a name="to-open-a-project"></a>Per aprire un progetto  
  
1.  Usare una delle procedure riportate di seguito:  
  
    1.  Nel **File** dal menu **progetti recenti**.  
  
    2.  Selezionare il progetto da aprire.  
  
    3.  Nel **File** dal menu **aprire il progetto**, individuare il file di progetto .m2ssproj, selezionare il file e quindi fare clic su **Open**.  
  
2.  Per ristabilire la connessione a MySQL nel **File** dal menu **Riconnetti a MySQL**.  
  
3.  Per ristabilire la connessione a SQL Server, sul **File** dal menu **Riconnetti a SQL Server**.  
  
4.  Per riconnettersi a SQL Azure, nelle **File** dal menu **ristabilire la connessione a SQL Azure.**  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[La connessione a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[La connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[La connessione al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
