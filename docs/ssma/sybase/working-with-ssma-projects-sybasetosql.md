---
title: Uso dei progetti SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: eb6f035b4d597e2b648134c195b698554dc78e12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072472"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Uso dei progetti SSMA (SybaseToSQL)
La migrazione dei database di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, creare innanzitutto un progetto SSMA. Il progetto è un file che contiene metadati sui database ambiente del servizio App che si desidera eseguire la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, i metadati relativi all'istanza di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure in cui verranno inseriti gli oggetti migrati e dati, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure informazioni di connessione e le impostazioni del progetto.  
  
Quando si apre un progetto, questo viene disconnesso dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Ciò consente di lavorare offline. È possibile riconnettersi alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Per altre informazioni, vedere [connessione a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [la connessione al database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Esame impostazioni predefinite del progetto  
SSMA contiene diverse opzioni per la conversione e il caricamento di oggetti di database, la migrazione dei dati e sincronizzazione di SSMA con ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Le impostazioni predefinite per queste opzioni sono appropriate per molti utenti. Tuttavia, prima di creare un nuovo progetto SSMA, si deve esaminare le opzioni e, se si desidera, modificare le impostazioni predefinite che verranno usate per tutti i nuovi progetti.  
  
**Per controllare le impostazioni di progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu **impostazioni di progetto predefinite**.  
  
2.  Selezionare il tipo di progetto in **versione di destinazione della migrazione** elenco a discesa per le impostazioni che deve essere visualizzati o modificati e quindi fare clic su **generali** scheda.  
  
3.  Nel riquadro sinistro, fare clic su **conversione**.  
  
4.  Nel riquadro di destra, esaminare le opzioni per modificare le opzioni in base alle esigenze. Per altre informazioni su queste opzioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Ripetere i passaggi da 1 a 3 per le pagine di migrazione, SQL Azure, il caricamento di oggetti, interfaccia utente grafica e del mapping dei tipi.  
  
    -   Per informazioni sulle opzioni di migrazione, vedere [impostazioni del progetto &#40;migrazione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Per informazioni sulle opzioni per il caricamento di oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [impostazioni di progetto &#40;sincronizzazione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Per altre informazioni sulle opzioni interfaccia utente grafica, vedere [impostazioni del progetto &#40;interfaccia utente grafica&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Per altre informazioni sulle impostazioni di mapping dei tipi di dati, fare clic su [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Per altre informazioni sulle opzioni di SQL Azure, vedere [impostazioni del progetto &#40;database SQL di Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > Le impostazioni di SQL Azure verranno visualizzate solo quando si seleziona **migrazione a SQL Azure** durante la creazione di un progetto.  
  
## <a name="creating-new-projects"></a>Creazione di nuovi progetti  
Per eseguire la migrazione dei dati dal database di ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è necessario creare innanzitutto un progetto.  
  
**Per creare un progetto**  
  
1.  Nel menu **File** selezionare **Nuovo progetto**.  
  
    Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nel **nome** immettere un nome per il progetto.  
  
3.  Nel **posizione** casella, immettere o selezionare una cartella per il progetto.  
  
4.  Nel **migrazione a** elenco a discesa, selezionare la versione del server di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato per la migrazione. Le opzioni disponibili sono:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Database SQL di Azure  
  
E quindi fare clic su **OK**.  
  
## <a name="customizing-project-settings"></a>Personalizzazione delle impostazioni di progetto  
Oltre a definire impostazioni predefinite del progetto che si applicano a tutti i nuovi progetti SSMA, è possibile personalizzare le impostazioni per ogni progetto. Per altre informazioni, vedere [impostazione delle opzioni progetto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Quando si personalizzano i mapping tra i database di origine e di destinazione, è possibile definire i mapping per il progetto, database o a livello di oggetto. Per altre informazioni sul mapping dei tipi, vedere [Mapping di Sybase ASE e SQL Server Data Types &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Il salvataggio dei progetti  
Quando si salva un progetto, SSMA consente di mantenere le impostazioni del progetto e, facoltativamente, i metadati del database, al file di progetto.  
  
**Per salvare un progetto**  
  
-   Nel **File** dal menu **Salva progetto**.  
  
    Se i database all'interno del progetto sono stati modificati o non sono stati convertiti, SSMA richiederà di salvare i metadati nel progetto. Salvataggio dei metadati consente di lavorare offline e l'invio di un file di progetto completo ad altri utenti, tra cui il personale di supporto tecnico. Se viene chiesto di salvare i metadati, eseguire le operazioni seguenti:  
  
    1.  Per ogni database che viene visualizzato lo stato **i metadati mancanti**, selezionare la casella di controllo accanto al nome del database.  
  
        Salvataggio di metadati potrebbe richiedere alcuni minuti. Se non si desidera salvare i metadati a questo punto, non selezionare le caselle di controllo.  
  
    2.  Fare clic sul pulsante **Salva**.  
  
        Analizza gli schemi di Sybase ASE e salvare i metadati del file di progetto SSMA.  
  
## <a name="opening-projects"></a>Apertura di progetti  
Quando si apre un progetto, questo viene disconnesso dall'ambiente del servizio App e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Ciò consente di lavorare offline. Per aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Per eseguire la migrazione dei dati, è necessario riconnettersi all'ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
**Per aprire un progetto**  
  
1.  Usare una delle procedure riportate di seguito:  
  
    -   Nel **File** dal menu **progetti recenti**e quindi selezionare il progetto da aprire.  
  
    -   Nel **File** dal menu **aprire il progetto**, individuare il file di progetto .s2ssproj, selezionare il file e quindi fare clic su **Open**.  
  
2.  Per riconnettersi all'ambiente del servizio App, nelle **File** dal menu **Riconnetti a Sybase**.  
  
3.  Per riconnettersi al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, nelle **File** dal menu **Riconnetti a SQL Server** / **Riconnetti a SQL Azure**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [connettersi a Sybase ASE](connecting-to-sybase-ase-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Connessione a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[La connessione a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[La connessione al database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
