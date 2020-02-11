---
title: Migrazione guidata (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 658487186924fe5547edee70425524b2b4e3be6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083587"
---
# <a name="migration-wizard-accesstosql"></a>Migrazione guidata (AccessToSQL)
La migrazione guidata consente di eseguire la migrazione di uno o più database dall'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Utilizzando la procedura guidata, si creerà un progetto, si aggiungeranno database al progetto, si selezionano gli oggetti di cui eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la migrazione e ci si connetterà a o SQL Azure. Sarà inoltre possibile convertire, caricare ed eseguire la migrazione di schemi e dati di accesso. Facoltativamente, è possibile collegare le tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso a o SQL Azure tabelle.  
  
La maggior parte delle pagine della migrazione guidata contiene le stesse opzioni delle finestre di dialogo SSMA esistenti. Pertanto, le pagine della procedura guidata sono descritte di seguito, quindi vengono forniti collegamenti per poter ottenere ulteriori informazioni sulle singole opzioni. Se una pagina contiene opzioni univoche, queste sono documentate qui.  
  
## <a name="starting-the-migration-wizard"></a>Avvio della migrazione guidata  
Per impostazione predefinita, la migrazione guidata viene visualizzata all'avvio di SSMA. È inoltre possibile avviare la procedura guidata dal menu **file** selezionando **migrazione guidata**.  
  
## <a name="welcome-page"></a>Home page  
Nella pagina iniziale è stata introdotta la procedura guidata di migrazione e viene fornita l'opzione seguente per avviare la procedura guidata.  
  
**Avvia la procedura guidata all'avvio.**  
Per impostazione predefinita, SSMA avvierà la migrazione guidata quando si avvia SSMA. Per evitare l'avvio automatico della procedura guidata, deselezionare questa casella di controllo.  
  
## <a name="create-new-project-page"></a>Pagina Crea nuovo progetto  
La pagina Crea nuovo progetto consente di immettere il nome del file di progetto, il percorso e il tipo di progetto di migrazione (la versione di destinazione SQL Server utilizzata per la migrazione). Per ulteriori informazioni, vedere [nuovo progetto (SSMA)](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Pagina Aggiungi database di accesso  
Nella pagina Aggiungi database di accesso è possibile aggiungere uno o più database di Access al progetto. È possibile aggiungere singoli database facendo clic su **Aggiungi database**, quindi selezionando i database dalla finestra **Apri** . In alternativa, è possibile trovare i database usando il pulsante **trova database** . Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Aggiunta e rimozione di file di database di Access](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [Procedura guidata per la ricerca di database (selezione percorsi)](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Procedura guidata per la ricerca di database (selezione file)](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Procedura guidata per la ricerca di database (verifica selezione)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Pagina Seleziona oggetti da migrare  
Nella pagina Seleziona oggetti da migrare è possibile selezionare gli oggetti da convertire. È possibile selezionare tutti gli oggetti, i gruppi di oggetti o singoli oggetti.  
  
**Per selezionare gli oggetti**  
  
1.  Espandere **Access-metabase**, quindi espandere **database**.  
  
2.  Eseguire almeno una fra le seguenti operazioni:  
  
    -   Per convertire tutti i database, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere i singoli database, selezionare o deselezionare la casella di controllo accanto al nome del database.  
  
    -   Per convertire o omettere le query, espandere il database, quindi selezionare o deselezionare la casella di controllo **query** .  
  
    -   Per convertire o omettere singole tabelle, espandere il database, espandere **tabelle**, quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
Se si dispone di molti oggetti, è possibile utilizzare le opzioni **avanzate di selezione oggetti** nel riquadro destro per filtrare gli oggetti di database di Access. Se, ad esempio, si selezionano **tabelle** nel riquadro sinistro, sarà possibile filtrare l'elenco delle tabelle immettendo le stringhe nella casella **filtro** . È quindi possibile selezionare o deselezionare le tabelle filtrate per la migrazione utilizzando i pulsanti nella parte superiore del riquadro.  
  
Per ulteriori informazioni sui filtri, vedere la sezione Opzioni di [selezione avanzata degli oggetti (SSMA Common)](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Connetti a SQL Server pagina  
Nella pagina Connetti a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificare le proprietà di connessione e quindi connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere [Connect to SQL Server](connect-to-sql-server-accesstosql.md).
  
> [!IMPORTANT]  
> Non appena la connessione ha esito positivo, si verificherà la pagina delle **tabelle dei collegamenti** in cui è possibile collegare le tabelle. Fare clic su **Avanti** per avviare la migrazione.  
  
## <a name="connect-to-sql-azure-page"></a>Connetti a SQL Azure pagina  
Nella pagina Connetti a SQL Azure è possibile specificare le proprietà di connessione e quindi connettersi a SQL Azure. Per creare un nuovo database di Azure, è possibile usare l'opzione **Crea database di Azure** che viene visualizzata facendo clic sul pulsante **Sfoglia** . Per ulteriori informazioni, vedere [Connect to SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> Non appena la connessione ha esito positivo, si verificherà la pagina delle **tabelle dei collegamenti** in cui è possibile collegare le tabelle. Fare clic sul pulsante **Avanti** nella pagina collegamenti per avviare la migrazione.  
  
## <a name="link-tables-page"></a>Pagina delle tabelle di collegamento  
Nella pagina tabelle dei collegamenti è possibile collegare le tabelle di accesso originali alle tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migrate o SQL Azure. Le tabelle di collegamento modificano il database di Access in modo che nelle query, nei form, nei report e nelle pagine di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso ai dati vengano utilizzati i dati nel database di o SQL Azure anziché i dati nel database di Access.  
  
**Tabelle di collegamento**  
Selezionare la casella di controllo **tabelle di collegamento** per collegare le tabelle di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle tabelle migrate o SQL Azure. Per avviare la migrazione, fare clic sul pulsante **Avanti** .  
  
## <a name="migration-status-page"></a>Pagina stato migrazione  
Nella pagina stato migrazione viene visualizzato lo stato di avanzamento della conversione degli schemi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di accesso in o SQL Azure schemi, il caricamento degli schemi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertiti in o SQL Azure, quindi la migrazione dei dati.  
  
Per ulteriori informazioni su questa pagina, vedere [Convert, Load e migrate](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione con SQL Server Migration Assistant per Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Guida di riferimento all'interfaccia utente (accesso)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
