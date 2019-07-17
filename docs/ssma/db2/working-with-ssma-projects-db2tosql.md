---
title: Uso dei progetti SSMA (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d2c585764e5bb7fffa55624054aecc7a4c589bbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086183"
---
# <a name="working-with-ssma-projects-db2tosql"></a>Uso dei progetti SSMA (DB2ToSQL)
Per eseguire la migrazione di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], creare innanzitutto un progetto SSMA. Il progetto è un file che contiene le informazioni seguenti:  
  
-   I metadati relativi a database DB2 si vuole eseguire la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   I metadati sull'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che riceverà i dati e oggetti migrati.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni di connessione.  
  
-   Impostazioni del progetto.  
  
Quando si apre un progetto, questo viene disconnesso da DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Che consente di lavorare offline. Per informazioni su riconnessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [ci si connette a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Esame impostazioni predefinite del progetto  
SSMA contiene diverse impostazioni per la conversione e il caricamento di oggetti di database, la migrazione dei dati e sincronizzazione SSMA con DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le impostazioni predefinite sono appropriate per molti utenti. Tuttavia, prima di creare un nuovo progetto SSMA, è consigliabile verificare le impostazioni. Se si desidera, è possibile modificare le impostazioni predefinite che verranno usate per tutti i nuovi progetti.  
  
**Per controllare le impostazioni di progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu fare clic su **impostazioni di progetto predefinite**.  
  
2.  Selezionare il tipo di progetto in **versione di destinazione della migrazione** elenco a discesa per le impostazioni che deve essere visualizzati o modificati e quindi fare clic su **generali** scheda.  
  
3.  Nel riquadro sinistro, fare clic su **conversione**.  
  
4.  Nel riquadro di destra, esaminare e modificare le impostazioni in base alle esigenze. Per altre informazioni su queste impostazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
5.  Ripetere i passaggi da 1 a 3 per le pagine di migrazione, la sincronizzazione, il caricamento di oggetti di sistema, interfaccia utente grafica e del mapping dei tipi.  
  
    -   Per informazioni sulle impostazioni di migrazione, vedere [impostazioni del progetto &#40;migrazione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md).  
  
    -   Per informazioni sulle impostazioni di oggetto di sistema, vedere [impostazioni del progetto&#40;caricamento oggetti di sistema&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md).  
  
    -   Per informazioni sulle impostazioni per la sincronizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [impostazioni di progetto&#40;sincronizzazione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
    -   Per informazioni sulle impostazioni di interfaccia utente grafica, vedere [impostazioni del progetto &#40;interfaccia utente grafica&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md).  
  
    -   Per informazioni sulle impostazioni di mapping dei tipi di dati, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="creating-new-projects"></a>Creazione di nuovi progetti  
Eseguire la migrazione dei dati da database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è innanzitutto necessario creare un progetto.  
  
**Per creare un progetto**  
  
1.  Scegliere **Nuovo progetto** dal menu **File**.  
  
    Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nel **nome** immettere un nome per il progetto.  
  
3.  Nel **ubicazione** casella, immettere o selezionare una cartella per il progetto e quindi fare clic su **OK**.  
  
4.  Nel **migrazione a** elenco a discesa, selezionare la versione del server di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato per la migrazione. Le opzioni disponibili sono:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Database SQL di Azure  
  
## <a name="customizing-project-settings"></a>Personalizzazione delle impostazioni di progetto  
Oltre a definire impostazioni predefinite del progetto che si applicano a tutti i nuovi progetti SSMA, è possibile personalizzare le impostazioni per ogni progetto. Per altre informazioni, vedere [impostazione delle opzioni progetto &#40;OracleToSQL&#41; ](../../ssma/oracle/setting-project-options-oracletosql.md) e relative sezioni.  
  
Quando si personalizzano i mapping tra i database di origine e di destinazione, è possibile definire i mapping per il progetto, database o a livello di oggetto. Per altre informazioni, vedere [Mapping di DB2 e tipi di dati di SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
## <a name="saving-projects"></a>Il salvataggio dei progetti  
Quando si salva un progetto, SSMA consente di mantenere le impostazioni del progetto e, facoltativamente, i metadati del database, al file di progetto.  
  
**Per salvare un progetto**  
  
-   Nel **File** menu, fare clic su **Salva progetto**.  
  
    Se gli schemi nel progetto sono stati modificati o non sono stati convertiti, SSMA richiederà di caricare e salvare i metadati. Il caricamento e salvataggio dei metadati consente di lavorare offline. Consente inoltre di inviare un file di progetto completo ad altre persone, ad esempio il personale di supporto tecnico. Se viene chiesto di salvare i metadati, eseguire le operazioni seguenti:  
  
    1.  Per ogni schema che mostra lo stato **i metadati mancanti**, selezionare la casella di controllo accanto al nome del database.  
  
        Salvataggio di metadati potrebbe richiedere alcuni minuti. Se non si desidera salvare i metadati, non selezionare le caselle di controllo.  
  
    2.  Fare clic sul pulsante **Salva**.  
  
        Analizza gli schemi DB2 e salvare i metadati del file di progetto SSMA.  
  
## <a name="opening-projects"></a>Apertura di progetti  
Quando si apre un progetto, questo viene disconnesso da DB2 e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Che consente di lavorare offline. Per aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per eseguire la migrazione dei dati, è necessario ristabilire la connessione a DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per aprire un progetto**  
  
1.  Usare una delle procedure riportate di seguito:  
  
    -   Nel **File** dal menu **progetti recenti**e quindi fare clic con il progetto da aprire.  
  
    -   Nel **File** dal menu **aprire il progetto**, individuare il file di progetto .o2ssproj, selezionare il file e quindi fare clic su **Open**.  
  
2.  Per ristabilire la connessione a DB2, nelle **File** menu, fare clic su **Riconnetti a DB2**.  
  
3.  Per riconnettersi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]via il **File** dal menu fare clic su **Riconnetti a SQL Server**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [ci si connette al Database DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
## <a name="see-also"></a>Vedere anche  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[La connessione al Database DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[La connessione a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
