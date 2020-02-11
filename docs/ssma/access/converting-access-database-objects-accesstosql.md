---
title: Conversione di oggetti di database di Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 56c55dbc5df61bfdb9013e505335af16fccbeecd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006625"
---
# <a name="converting-access-database-objects-accesstosql"></a>Conversione di oggetti di database di Access (AccessToSQL)
Dopo aver aggiunto i database di Access e aver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] effettuato la connessione a o SQL Azure, SSMA Visualizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i metadati per l'accesso e o SQL Azure oggetti di database. È ora possibile selezionare Access Database Objects, quindi convertire gli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure schemi.  
  
## <a name="the-conversion-process"></a>Processo di conversione  
La conversione di oggetti di database accetta le definizioni degli oggetti dai metadati di accesso, [!INCLUDE[tsql](../../includes/tsql-md.md)] le converte in sintassi equivalente e quindi carica tali informazioni nel progetto. È quindi possibile visualizzare gli [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti o SQL Azure e le relative proprietà tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure Esplora metadati.  
  
> [!IMPORTANT]  
> La conversione di oggetti non comporta la creazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] degli oggetti in o SQL Azure. Converte solo le definizioni di oggetto e archivia le informazioni nel progetto SSMA.  
  
Durante la conversione, SSMA stampa lo stato nel riquadro di output e i messaggi di errore, di avviso e informativi nel riquadro Elenco errori. Usare queste informazioni per determinare se è necessario modificare i database di Access o il processo di conversione per ottenere i risultati della conversione desiderati. È inoltre possibile utilizzare le informazioni contenute nell'argomento [preparazione dei database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md) per determinare gli elementi che non verranno convertiti.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione del progetto nella finestra di dialogo **Impostazioni progetto** . Utilizzando questa finestra di dialogo è possibile impostare il modo in cui SSMA converte le colonne Memo indicizzate, le chiavi primarie, i vincoli di chiave esterna, i timestamp e le tabelle senza indici. Per ulteriori informazioni, vedere [Impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Risultati della conversione  
Nella tabella seguente vengono illustrati gli oggetti di accesso che vengono convertiti e gli oggetti risultanti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure:  
  
|Oggetto Access|Oggetto SQL Server risultante|  
|-----------------|-------------------------------|  
|tabella|tabella|  
|colonna|colonna|  
|indice|indice|  
|chiave esterna|chiave esterna|  
|query|vista<br /><br />La maggior parte delle query SELECT viene convertita in viste. Non viene eseguita la migrazione di altre query, ad esempio query di aggiornamento.<br /><br />Le query SELECT che accettano parametri non vengono convertite, né query tra tabulazioni.|  
|report|non convertito|  
|form|non convertito|  
|macro|non convertito|  
|modulo|non convertito|  
|valore predefinito|valore predefinito|  
|Consenti proprietà colonna a lunghezza zero|vincolo check|  
|regola di convalida colonne|vincolo check|  
|regola di convalida tabella|vincolo check|  
|chiave primaria|chiave primaria|  
  
## <a name="converting-access-objects"></a>Conversione di oggetti Access  
Per convertire gli oggetti di database di Access, è necessario innanzitutto selezionare gli oggetti che si desidera convertire, quindi fare in modo che SSMA esegua la conversione. Per visualizzare i messaggi di output durante la conversione, scegliere **output**dal menu **Visualizza** .  
  
**Per selezionare e convertire gli oggetti di database di Access in SQL Server o SQL Azure sintassi**  
  
1.  In Esplora metadati di Access espandere **Access-metabase**, quindi espandere **database**.  
  
2.  Eseguire almeno una fra le seguenti operazioni:  
  
    -   Per convertire tutti i database, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere i singoli database, selezionare o deselezionare la casella di controllo accanto al nome del database.  
  
    -   Per convertire o omettere le query, espandere il database, quindi selezionare o deselezionare la casella di controllo **query** .  
  
    -   Per convertire o omettere singole tabelle, espandere il database, espandere **tabelle**, quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
3.  Eseguire una delle operazioni seguenti:  
  
    -   Per convertire gli schemi, fare clic con il pulsante destro del mouse su **database** e scegliere **Converti schema**.  
  
        È anche possibile convertire singoli oggetti. Per convertire un oggetto, indipendentemente dagli oggetti selezionati, fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Converti schema**.  
  
        Quando un oggetto è stato convertito, viene visualizzato in grassetto in Esplora metadati di Access.  
  
    -   Per convertire, caricare ed eseguire la migrazione di schemi e dati in un unico passaggio, fare clic con il pulsante destro del mouse su database e scegliere **Converti, carica ed Esegui migrazione**.  
  
4.  Esaminare i messaggi nel riquadro di **output** e gli eventuali errori e avvisi nel riquadro **Elenco errori** .  
  
## <a name="altering-tables-and-indexes"></a>Modifica di tabelle e indici  
Dopo aver convertito i metadati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] accesso a o SQL Azure metadati e prima di caricare gli oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in o SQL Azure, è possibile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modificare o SQL Azure tabelle e indici.  
  
**Per modificare le proprietà di tabelle o indici**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure Esplora metadati selezionare la tabella o l'indice che si desidera modificare.  
  
2.  Nella scheda **tabella** fare clic sulla proprietà che si desidera modificare, quindi immettere o selezionare la nuova impostazione. Ad esempio, è possibile modificare nvarchar (15) in nvarchar (20) o selezionare una casella di controllo per rendere Nullable una colonna della tabella.  
  
    Spostare il cursore all'esterno della cella della proprietà modificata. A tale scopo, fare clic su un'altra riga o premere il tasto TAB.  
  
3.  Fare clic su **Apply**.  
  
È ora possibile visualizzare le modifiche nel codice nella scheda **SQL** .  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo del processo di migrazione consiste nel [caricare gli oggetti di database convertiti in SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
