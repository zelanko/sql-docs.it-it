---
title: Impostazione delle opzioni progetto (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2c8d074db2fc1e8a9d29ecf5fdc0405524e9bb1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020924"
---
# <a name="setting-project-options-sybasetosql"></a>Impostazione delle opzioni del progetto (SybaseToSQL)
Per ogni progetto SSMA, è possibile impostare le opzioni a livello di progetto. Queste opzioni specificano la conversione degli oggetti, il caricamento di oggetti, SQL azure, interfaccia utente e le impostazioni di migrazione dei dati. Prima di convertire gli oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure o eseguire la migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, verificare che le opzioni di configurazione siano appropriate per il progetto.  
  
SSMA consente di configurare le opzioni predefinite per tutti i progetti. Queste opzioni vengono applicate a qualsiasi nuovo progetto creato. È quindi possibile personalizzare le opzioni per ogni progetto.  
  
## <a name="configuration-options-and-modes"></a>Le modalità e le opzioni di configurazione  
SSMA è cinque set di impostazioni di progetto:  
  
1.  Informazioni sul progetto  
  
2.  Generale (conversione, migrazione e la raccolta dei dati)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  Mapping dei tipi  
  
Include inoltre quattro modalità per la configurazione di queste impostazioni:  
  
1.  Impostazione predefinita  
  
2.  Optimistic  
  
3.  Full  
  
4.  Personalizzato  
  
La modalità predefinita è consigliata per la maggior parte degli utenti. La modalità ottimistica mantiene più la sintassi di Sybase Adaptive Server Enterprise (ASE) corrente e facile da leggere. Tuttavia, mantenendo la sintassi corrente potrebbe non essere accurata. Se la sintassi di ambiente del servizio App devono essere convertita in equivalenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintassi di SQL Azure, la modalità completa esegue una conversione completa, ma il codice risulta potrebbe essere più difficile da leggere. Nella modalità personalizzata, impostare le opzioni.  
  
Le impostazioni sono descritte nella sezione riferimenti dell'interfaccia utente di questa documentazione. Per altre informazioni sulle impostazioni e come vengono applicate le impostazioni in ciascuna modalità, vedere gli argomenti seguenti:  
  
-   [Le impostazioni di progetto &#40;conversione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Le impostazioni di progetto &#40;migrazione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Le impostazioni di progetto &#40;sincronizzazione&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Le impostazioni di progetto &#40;interfaccia utente grafica&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Le impostazioni di progetto &#40;Mapping dei tipi&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Le impostazioni di progetto &#40;Azure SQL database &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Impostazione delle opzioni del progetto  
In SSMA, è possibile configurare le impostazioni predefinite per tutti i progetti. Queste impostazioni vengono salvate nel file di configurazione di SSMA e applicate a ogni nuovo progetto creato.  
  
**Per impostare le opzioni del progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu **impostazioni di progetto predefinite**.  
  
2.  Nel **impostazioni di progetto predefinite** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    -   Seleziona tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati dal **versione di destinazione della migrazione** drop verso il basso fare clic su Generale nella parte inferiore del riquadro di sinistra e quindi selezionare la conversione o la migrazione o di SQL Azure.  
  
    -   Per selezionare una modalità predefinita, il **modalità** casella di riepilogo a discesa, selezionare **predefinito**, **Optimistic**, o **completo**.  
  
    -   Per specificare le impostazioni personalizzate, è sufficiente selezionare o immettere le nuove impostazioni o i valori.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
È anche possibile personalizzare le impostazioni per il progetto corrente. Queste impostazioni vengono salvate nel file di progetto corrente.  
  
**Per personalizzare le impostazioni per il progetto corrente**  
  
1.  Nel **degli strumenti** dal menu **le impostazioni del progetto**.  
  
2.  Nel **impostazioni del progetto** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    -   Per selezionare una modalità predefinita, il **modalità** casella di riepilogo a discesa, selezionare **predefinito**, **Optimistic**, o **completo**.  
  
    -   Per specificare una modalità personalizzata, nelle **modalità** elenco a discesa, selezionare **personalizzato**selezionare un'opzione nel riquadro sinistro, fare clic sull'impostazione o un valore nel riquadro di destra e quindi selezionare o immettere il valore o la nuova impostazione.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Se si vuole su personalizzato il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di Sybase ASE e SQL Server Data Types &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   In caso contrario, è possibile convertire le definizioni degli oggetti di database Sybase in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o le definizioni degli oggetti di SQL Azure. Per altre informazioni, vedere [convertire gli oggetti di Database di Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
