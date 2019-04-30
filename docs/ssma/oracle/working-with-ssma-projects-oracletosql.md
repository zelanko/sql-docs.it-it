---
title: Uso dei progetti SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 3ec3a2f9bcdf43657649263d77eff3b31c9a57a3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283555"
---
# <a name="working-with-ssma-projects-oracletosql"></a>Uso dei progetti SSMA (OracleToSQL)
Eseguire la migrazione di database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], creare innanzitutto un progetto SSMA. Il progetto è un file che contiene le informazioni seguenti:  
  
-   I metadati relativi a database Oracle si vuole eseguire la migrazione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   I metadati sull'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che riceverà i dati e oggetti migrati.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni di connessione.  
  
-   Impostazioni del progetto.  
  
Quando si apre un progetto, si viene disconnessi da Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Che consente di lavorare offline. Per informazioni su riconnessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [ci si connette a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Esame impostazioni predefinite del progetto  
SSMA contiene diverse impostazioni per la conversione e il caricamento di oggetti di database, la migrazione dei dati e sincronizzazione di SSMA con Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le impostazioni predefinite sono appropriate per molti utenti. Tuttavia, prima di creare un nuovo progetto SSMA, è consigliabile verificare le impostazioni. Se si desidera, è possibile modificare le impostazioni predefinite che verranno usate per tutti i nuovi progetti.  
  
**Per controllare le impostazioni di progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu fare clic su **impostazioni di progetto predefinite**.  
  
2.  Selezionare il tipo di progetto in **versione di destinazione della migrazione** elenco a discesa per le impostazioni che deve essere visualizzati o modificati e quindi fare clic su **generali** scheda.  
  
3.  Nel riquadro sinistro, fare clic su **conversione**.  
  
4.  Nel riquadro di destra, esaminare e modificare le impostazioni in base alle esigenze. Per altre informazioni su queste impostazioni, vedere [impostazioni del progetto &#40;conversione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Ripetere i passaggi da 1 a 3 per le pagine di migrazione, la sincronizzazione, il caricamento di oggetti di sistema, interfaccia utente grafica e del mapping dei tipi.  
  
    -   Per informazioni sulle impostazioni di migrazione, vedere [impostazioni del progetto &#40;migrazione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Per informazioni sulle impostazioni di oggetto di sistema, vedere [impostazioni del progetto&#40;caricamento oggetti di sistema&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Per informazioni sulle impostazioni per la sincronizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [impostazioni di progetto&#40;sincronizzazione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Per informazioni sulle impostazioni di interfaccia utente grafica, vedere [impostazioni del progetto &#40;interfaccia utente grafica&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Per informazioni sulle impostazioni di mapping dei tipi di dati, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Creazione di nuovi progetti  
Eseguire la migrazione dei dati da database Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è innanzitutto necessario creare un progetto.  
  
**Per creare un progetto**  
  
1.  Nel **File** menu, fare clic su **nuovo progetto**.  
  
    Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nel **nome** immettere un nome per il progetto.  
  
3.  Nel **ubicazione** casella, immettere o selezionare una cartella per il progetto e quindi fare clic su **OK**.  
  
4.  Nel **migrazione a** elenco a discesa, selezionare la versione del server di destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato per la migrazione. Le opzioni disponibili sono:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Database SQL di Azure  
  
## <a name="customizing-project-settings"></a>Personalizzazione delle impostazioni di progetto  
Oltre a definire impostazioni predefinite del progetto che si applicano a tutti i nuovi progetti SSMA, è possibile personalizzare le impostazioni per ogni progetto. Per altre informazioni, vedere [impostazione delle opzioni progetto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Quando si personalizzano i mapping tra i database di origine e di destinazione, è possibile definire i mapping per il progetto, database o a livello di oggetto. Per altre informazioni, vedere [Mapping di Oracle e SQL Server Data Types &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Il salvataggio dei progetti  
Quando si salva un progetto, SSMA consente di mantenere le impostazioni del progetto e, facoltativamente, i metadati del database, al file di progetto.  
  
**Per salvare un progetto**  
  
-   Nel **File** menu, fare clic su **Salva progetto**.  
  
    Se gli schemi nel progetto sono stati modificati o non sono stati convertiti, SSMA richiederà di caricare e salvare i metadati. Il caricamento e salvataggio dei metadati consente di lavorare offline. Consente inoltre di inviare un file di progetto completo ad altre persone, ad esempio il personale di supporto tecnico. Se viene chiesto di salvare i metadati, eseguire le operazioni seguenti:  
  
    1.  Per ogni schema che mostra lo stato **i metadati mancanti**, selezionare la casella di controllo accanto al nome del database.  
  
        Salvataggio di metadati potrebbe richiedere alcuni minuti. Se non si desidera salvare i metadati, non selezionare le caselle di controllo.  
  
    2.  Fare clic sul pulsante **Salva**.  
  
        Analizza gli schemi di Oracle e salvare i metadati del file di progetto SSMA.  
  
## <a name="opening-projects"></a>Apertura di progetti  
Quando si apre un progetto, questo viene disconnesso da Oracle e da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Che consente di lavorare offline. Per aggiornare i metadati, caricare gli oggetti di database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per eseguire la migrazione dei dati, è necessario riconnettersi a Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Per aprire un progetto**  
  
1.  Usare una delle procedure riportate di seguito:  
  
    -   Nel **File** dal menu **progetti recenti**e quindi fare clic con il progetto da aprire.  
  
    -   Nel **File** dal menu **aprire il progetto**, individuare il file di progetto .o2ssproj, selezionare il file e quindi fare clic su **Open**.  
  
2.  Per ristabilire la connessione a Oracle, nelle **File** menu, fare clic su **Riconnetti a Oracle**.  
  
3.  Per riconnettersi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]via il **File** dal menu fare clic su **Riconnetti a SQL Server**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [la connessione al Database Oracle (OracleToSQL)](https://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[La connessione al Database Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[La connessione a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
