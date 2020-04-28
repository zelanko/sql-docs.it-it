---
title: Creazione e gestione di progetti (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: abbe0746193df3fe341b4f66086291dc1055e11b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006614"
---
# <a name="creating-and-managing-projects-accesstosql"></a>Creazione e gestione di progetti (AccessToSQL)
Per eseguire la migrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a o SQL Azure, è necessario creare prima un progetto SSMA. Il progetto è un file contenente i metadati relativi ai database di Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui si desidera eseguire la migrazione o SQL Azure, i metadati relativi all' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di destinazione di o SQL Azure che riceveranno gli oggetti e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i dati migrati, le informazioni di connessione e le impostazioni del progetto.  
  
## <a name="reviewing-default-project-settings"></a>Revisione delle impostazioni predefinite del progetto  
SSMA contiene diverse opzioni per la conversione e la sincronizzazione degli oggetti di database e per la conversione dei dati. L'impostazione predefinita per queste opzioni è appropriata per molti utenti. Tuttavia, prima di creare un nuovo progetto SSMA, è necessario rivedere le opzioni e, se si vuole, modificare le impostazioni predefinite che verranno usate per tutti i nuovi progetti.  
  
**Per esaminare le impostazioni predefinite del progetto**  
  
1.  Scegliere **Impostazioni progetto predefinite**dal menu **strumenti** .  
  
2.  Selezionare il tipo di progetto nell'elenco a discesa della **versione di destinazione della migrazione** per cui visualizzare o modificare le impostazioni e quindi fare clic sulla scheda **generale** .  
  
3.  Nel riquadro sinistro fare clic su **conversione**.  
  
4.  Nel riquadro destro esaminare le opzioni. Per ulteriori informazioni su queste opzioni, vedere [Impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Modificare le opzioni in modo necessario.  
  
6.  Ripetere i passaggi precedenti per le pagine **migrazione**, **GUI**e **mapping dei tipi** .  
  
    -   Per informazioni sulle opzioni di migrazione, vedere [Impostazioni progetto (migrazione)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Per informazioni sulle opzioni dell'interfaccia utente, vedere [Impostazioni progetto (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Per ulteriori informazioni sulle impostazioni di mapping dei tipi di dati, vedere [Impostazioni progetto (mapping dei tipi)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Per informazioni sulle impostazioni di SQL Azure, vedere [Impostazioni progetto (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Nota** SQL Azure impostazioni saranno disponibili solo quando si seleziona la migrazione per SQL Azure durante la creazione di un progetto.  
  
## <a name="creating-new-projects"></a>Creazione di nuovi progetti  
SSMA inizia senza caricare un progetto predefinito. Per eseguire la migrazione dei dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a o SQL Azure, è necessario creare un progetto.  
  
**Per creare un nuovo progetto**  
  
1.  Scegliere **Nuovo progetto** dal menu **File**.  
  
    Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
2.  Nella casella **nome** immettere un nome per il progetto.  
  
3.  Nella casella **percorso** immettere o selezionare una cartella per il progetto  
  
4.  Nell'elenco a discesa migrazione a selezionare uno dei SQL Server 2005/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016/database SQL di Azure e quindi fare clic su **OK**.  
  
SSMA crea il file di progetto. È ora possibile eseguire il passaggio successivo per [aggiungere uno o più database di Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="customizing-project-settings"></a>Personalizzazione delle impostazioni di progetto  
Oltre a definire le impostazioni di progetto predefinite, applicabili a tutti i nuovi progetti SSMA, è anche possibile personalizzare le impostazioni per ogni progetto. Per ulteriori informazioni, vedere [impostazione delle opzioni di conversione e migrazione](setting-conversion-and-migration-options-accesstosql.md).  
  
Quando si personalizzano i mapping dei tipi di dati tra i database di origine e di destinazione, è possibile definire i mapping a livello di progetto, database o oggetto. Per ulteriori informazioni sul mapping dei tipi, vedere [mapping di tipi di dati di origine e di destinazione](mapping-source-and-target-data-types-accesstosql.md).  
  
## <a name="saving-projects"></a>Salvataggio di progetti  
Quando si salva un progetto, SSMA Salva in modo permanente le impostazioni del progetto e, facoltativamente, i metadati del database, nel file di progetto.  
  
**Per salvare un progetto**  
  
-   Scegliere **Salva progetto**dal menu **file** .  
  
    Se i database all'interno del progetto sono stati modificati o non sono stati convertiti, SSMA richiede di salvare i metadati nel progetto. Salvando i metadati è possibile lavorare offline. Consente inoltre di inviare un file di progetto completo ad altre persone, incluso il personale del supporto tecnico. Se viene richiesto di salvare i metadati, procedere come segue:  
  
    1.  Per ogni database che mostra lo stato dei **metadati mancanti**, selezionare la casella di controllo accanto al nome del database.  
  
        Il salvataggio dei metadati potrebbe richiedere diversi minuti. Se non si desidera salvare i metadati in questa fase, non selezionare alcuna casella di controllo.  
  
    2.  Fare clic su **Salva**.  
  
        SSMA analizzerà gli schemi di accesso e salverà i metadati nel file di progetto.  
  
## <a name="opening-projects"></a>Apertura di progetti  
Quando si apre un progetto, questo viene disconnesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da o SQL Azure. In questo modo è possibile lavorare offline. Per aggiornare i metadati caricare oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database in o SQL Azure. Per eseguire la migrazione dei dati, è necessario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riconnettersi a o SQL Azure.  
  
**Per aprire un progetto**  
  
1.  Usare una delle procedure seguenti:  
  
    -   Scegliere **progetti recenti**dal menu **file** , quindi selezionare il progetto che si desidera aprire.  
  
    -   Nel menu **file** selezionare **Apri progetto**, individuare il file di progetto. a2ssproj, selezionare il file e quindi fare clic su **Apri**.  
  
2.  Per riconnettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], scegliere **riconnetti a SQL Server**dal menu **file** .  
  
3.  Per riconnettersi a SQL Azure, scegliere **Riconnetti a SQL Azure** dal menu **file** .  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo del processo di migrazione consiste nell' [aggiungere uno o più database di Access](adding-and-removing-access-database-files-accesstosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Aggiunta e rimozione di file di database di Access](adding-and-removing-access-database-files-accesstosql.md)  
  
