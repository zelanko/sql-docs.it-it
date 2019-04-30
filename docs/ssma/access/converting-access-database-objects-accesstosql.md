---
title: Conversione di oggetti di Database di Access (AccessToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c4bb3d1b6fdc57e1251e9c8ca39f0c7437ffb126
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63139022"
---
# <a name="converting-access-database-objects-accesstosql"></a>Conversione di oggetti di Database di Access (AccessToSQL)
Dopo aver aggiunto i database di Access e connesso al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, SSMA consente di visualizzare metadati per l'accesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oggetti di database di SQL Azure. È possibile selezionare gli oggetti di database di Access e quindi eseguire la conversione degli schemi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o degli schemi di SQL Azure.  
  
## <a name="the-conversion-process"></a>Il processo di conversione  
Conversione di oggetti di database richiede le definizioni degli oggetti da accedere ai metadati, li converte in equivalente [!INCLUDE[tsql](../../includes/tsql-md.md)] informazioni sulla sintassi e quindi carica tali informazioni nel progetto. È quindi possibile visualizzare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure e le relative proprietà utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure.  
  
> [!IMPORTANT]  
> Conversione di oggetti non crea gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Solo converte le definizioni degli oggetti e archivia le informazioni nel progetto SSMA.  
  
Durante la conversione SSMA viene stampato lo stato per il riquadro di Output ed errore, avviso e messaggi informativi per il riquadro elenco errori. Usare queste informazioni per determinare se è necessario modificare i database di Access o il processo di conversione per ottenere i risultati di conversione desiderato. È anche possibile usare le informazioni contenute nel [preparare i database di Access per la migrazione](preparing-access-databases-for-migration-accesstosql.md) argomento per determinare che cosa verrà e non verrà convertita.  
  
## <a name="setting-conversion-options"></a>Impostazione delle opzioni di conversione  
Prima di convertire gli oggetti, esaminare le opzioni di conversione progetto nel **impostazioni del progetto** nella finestra di dialogo. Tramite questa finestra di dialogo, è possibile impostare la modalità di conversione di colonne di tipo memo indicizzata, le chiavi primarie, vincoli di chiave esterna, i timestamp e tabelle senza indici in SSMA. Per altre informazioni, vedere [impostazioni progetto (conversione)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Risultati conversione  
La tabella seguente mostra quali oggetti di Access vengono convertiti e risultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure:  
  
|Oggetto di accesso|Oggetto risulta di SQL Server|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|indice|indice|  
|chiave esterna|chiave esterna|  
|Query|vista<br /><br />Le query più SELECT vengono convertite alle visualizzazioni. Altre query, ad esempio le query di aggiornamento, non vengono migrate.<br /><br />Query SELECT che accettano parametri non vengono convertite, né lo sono le query tra più schede.|  
|report|non convertito|  
|Form|non convertito|  
|macro|non convertito|  
|modulo|non convertito|  
|Valore predefinito|Valore predefinito|  
|Consenti zero proprietà lunghezza della colonna|vincolo CHECK|  
|regola di convalida di colonna|vincolo CHECK|  
|regola di convalida della tabella|vincolo CHECK|  
|chiave primaria|chiave primaria|  
  
## <a name="converting-access-objects"></a>Conversione di oggetti di accesso  
Per convertire gli oggetti di database di Access, è innanzitutto necessario selezionare gli oggetti a cui che si desidera convertire e quindi chiedere di SSMA eseguire la conversione. Per visualizzare i messaggi di output durante la conversione nel **View** dal menu **Output**.  
  
**Per selezionare e convertire gli oggetti di database l'accesso in sintassi SQL Server o SQL Azure**  
  
1.  Nel Visualizzatore metadati di accesso, espandere **accesso metabase**, quindi espandere **database**.  
  
2.  Eseguire una o più delle seguenti operazioni:  
  
    -   Per convertire tutti i database, selezionare la casella di controllo accanto a **database**.  
  
    -   Per convertire o omettere i singoli database, selezionare o deselezionare la casella di controllo accanto al nome del database.  
  
    -   Per convertire o omettere le query, espandere il database e quindi selezionare o deselezionare i **query** casella di controllo.  
  
    -   Per convertire o omettere le singole tabelle, espandere il database, espandere **tabelle**e quindi selezionare o deselezionare la casella di controllo accanto alla tabella.  
  
3.  Eseguire una delle operazioni seguenti:  
  
    -   Per convertire gli schemi, fare doppio clic su **database** e selezionare **Converti Schema**.  
  
        È anche possibile convertire i singoli oggetti. Per convertire un oggetto, indipendentemente dal fatto che siano selezionati gli oggetti, fare doppio clic su oggetto e selezionare **convertire lo Schema**.  
  
        Quando un oggetto è stato convertito, viene visualizzato in grassetto nel Visualizzatore metadati di accesso.  
  
    -   Per convertire, caricare e la migrazione di schemi e dati in un unico passaggio, fare doppio clic su database e selezionare **convertire, caricare ed eseguire la migrazione**.  
  
4.  Esaminare i messaggi nella **Output** riquadro e gli eventuali errori e avvisi nel **elenco errori** riquadro.  
  
## <a name="altering-tables-and-indexes"></a>Modifica di tabelle e indici  
Dopo la conversione di accedere ai metadati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o i metadati di SQL Azure, e prima di caricare gli oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è possibile modificare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tabelle di SQL Azure e gli indici.  
  
**Modificare le proprietà di tabella o un indice**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Visualizzatore metadati di SQL Azure, selezionare la tabella o indice da modificare.  
  
2.  Nel **tabella** scheda, fare clic sulla proprietà che si desidera modificare e quindi immettere o selezionare la nuova impostazione. Ad esempio, è possibile modificare nvarchar(15) nvarchar(20) o selezionare una casella di controllo per impostare una colonna di tabella che ammette valori null.  
  
    Spostare il cursore all'esterno della cella di proprietà modificata. È possibile farlo premendo il tasto Tab o facendo clic su un'altra riga.  
  
3.  Fare clic su **Applica**.  
  
È ora possibile visualizzare le modifiche nel codice nel **SQL** scheda.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [caricare gli oggetti di database convertiti in SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
