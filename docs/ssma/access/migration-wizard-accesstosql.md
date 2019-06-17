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
manager: craigg
ms.openlocfilehash: acb05f10772ebdf77355b78e1f4ce998cc6c8056
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63453545"
---
# <a name="migration-wizard-accesstosql"></a>Migrazione guidata (AccessToSQL)
La migrazione guidata consente la migrazione di uno o più database da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Usando la procedura guidata, verranno creare un progetto, aggiungere database al progetto, selezionare gli oggetti per eseguire la migrazione e connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È anche convertire, caricare e migrare i dati e schemi di accesso. Facoltativamente, è possibile collegare le tabelle di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle o di SQL Azure.  
  
La maggior parte delle pagine della procedura guidata di migrazione contengono le stesse opzioni di finestre di dialogo SSMA esistenti. Pertanto, le pagine della procedura guidata sono descritte di seguito, e quindi vengono forniti i collegamenti in modo che altre informazioni sulle singole opzioni. Se una pagina contiene le opzioni univoche, sono documentate qui.  
  
## <a name="starting-the-migration-wizard"></a>Avvio della procedura guidata di migrazione  
Per impostazione predefinita, la migrazione guidata viene visualizzata quando si avvia SSMA. È anche possibile avviare la procedura guidata nel **File** dal menu selezionando **migrazione guidata**.  
  
## <a name="welcome-page"></a>Pagina introduttiva  
La pagina di benvenuto presenta la procedura guidata di migrazione e fornisce l'opzione seguente per avviare la procedura guidata.  
  
**Avviare questa procedura guidata all'avvio.**  
Per impostazione predefinita, SSMA inizierà la migrazione guidata quando si avvia SSMA. Per impedire l'avvio automatico della procedura guidata, deselezionare questa casella di controllo.  
  
## <a name="create-new-project-page"></a>Creare una nuova pagina del progetto  
La pagina Crea nuovo progetto è dove inserire il progetto file nome, posizione e la migrazione tipo di progetto (la versione di SQL Server usato per la migrazione di destinazione). Per altre informazioni, vedere [nuovo progetto (SSMA)](https://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Aggiungi pagina di accesso ai database  
La pagina di aggiungere i database di Access è aggiungere una o più database di Access al progetto. È possibile aggiungere i singoli database facendo **aggiungere i database**e quindi selezionando i database dal **Open** finestra. In alternativa, è possibile trovare i database tramite il **trovare database** pulsante. Per altre informazioni, vedere i seguenti argomenti:  
  
-   [Aggiunta e rimozione di file di Database di Access](adding-and-removing-access-database-files-accesstosql.md)  
  
-   [Procedura guidata trova database (Seleziona percorsi)](https://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Procedura guidata trova database (Seleziona file)](https://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Procedura guidata Trova database (verifica selezione)](https://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Selezionare gli oggetti per eseguire la migrazione di pagina  
Per gli oggetti selezionare alla pagina di migrazione, si selezionano oggetti da convertire. È possibile selezionare tutti gli oggetti, gruppi di oggetti o singoli oggetti.  
  
**Per selezionare gli oggetti**  
  
1.  Espandere **accesso metabase**, quindi espandere **database**.  
  
2.  Eseguire una o più delle seguenti operazioni:  
  
    -   Per convertire tutti i database, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere i singoli database, selezionare o deselezionare la casella di controllo accanto al nome del database.  
  
    -   Per convertire o omettere le query, espandere il database e quindi selezionare o deselezionare i **query** casella di controllo.  
  
    -   Per convertire o omettere le singole tabelle, espandere il database, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
Se si dispone di molti oggetti, si potrebbe voler usare il **Selezione oggetto avanzata** opzioni nel riquadro di destra per filtrare l'accesso degli oggetti di database. Ad esempio, se si seleziona **tabelle** nel riquadro sinistro, è quindi possibile filtrare l'elenco di tabelle, immettere le stringhe nel **filtro** casella. È quindi possibile selezionare o deselezionare le tabelle filtrate per la migrazione usando i pulsanti nella parte superiore del riquadro.  
  
Per altre informazioni sui filtri, vedere la sezione Opzioni della [selezione di oggetti avanzati, SSMA comuni,](https://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Connettersi alla pagina SQL Server  
Nella finestra Connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pagina, specificare le proprietà di connessione e quindi connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Connetti al Server SQL](connect-to-sql-server-accesstosql.md).
  
> [!IMPORTANT]  
> Non appena la connessione ha esito positivo, si verificheranno **tabelle di collegamento** pagina in cui disponibile un'opzione di collegamento tra le tabelle. Fare clic su **successivo** e inizia la migrazione.  
  
## <a name="connect-to-sql-azure-page"></a>Connettersi a SQL Azure pagina  
Nella pagina Connetti a SQL Azure, specificare le proprietà di connessione e quindi connettersi a SQL Azure. Per creare un nuovo database di azure, è possibile farlo usando **Create Database di Azure** opzione che viene visualizzato in un semplice clic su **Sfoglia** pulsante. Per altre informazioni, vedere [Connetti a SQL Azure](connect-to-azure-sql-db-accesstosql.md)  
  
> [!IMPORTANT]  
> Non appena la connessione ha esito positivo, si verificheranno **tabelle di collegamento** pagina in cui disponibile un'opzione di collegamento tra le tabelle. Fare clic su **successivo** pulsante nella pagina di collegamenti per avviare la migrazione.  
  
## <a name="link-tables-page"></a>Pagina di tabelle di collegamento  
La pagina di tabelle di collegamento consente di collegare le tabelle di Access originale dopo la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure. Collegamento delle tabelle di modifica nel database di Access in modo che le pagine di accesso di query, form, i report e dati usano i dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure anziché i dati presenti nel database di Access.  
  
**Tabelle di collegamento**  
Selezionare il **collegare le tabelle** casella di controllo a cui collegarsi accedere alle tabelle dopo la migrazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure. Per avviare la migrazione è necessario fare clic su **successivo** pulsante.  
  
## <a name="migration-status-page"></a>Pagina di migrazione stato  
Pagina relativa allo stato di migrazione viene visualizzato lo stato di conversione gli schemi di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi di SQL Azure, il caricamento degli schemi convertiti in o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, e quindi migrare i dati.  
  
Per altre informazioni su questa pagina, vedere [convertire, caricare ed eseguire la migrazione](https://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Vedere anche  
[Introduzione a SQL Server Migration Assistant per Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Reference(Access) dell'interfaccia utente](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
