---
title: Impostazione delle opzioni progetto (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 7760a893082f7b4a8899e00480fc43914b1c12ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625915"
---
# <a name="setting-project-options-oracletosql"></a>Impostazione delle opzioni progetto (OracleToSQL)
Per ogni progetto SSMA è possibile impostare le opzioni a livello di progetto. Queste opzioni specificano la conversione degli oggetti, il caricamento di oggetti, impostazioni di migrazione di dati e dell'interfaccia utente. Prima di convertire gli oggetti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure eseguire la migrazione dei dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verificare che le opzioni di configurazione siano appropriate per il progetto.  
  
SSMA consente di configurare le opzioni predefinite per tutti i progetti. Queste opzioni vengono applicate a ogni nuovo progetto creato. È quindi possibile personalizzare le opzioni per ogni progetto.  
  
## <a name="configuration-options-and-modes"></a>Le modalità e le opzioni di configurazione  
SSMA è cinque set di impostazioni di progetto:  
  
-   Informazioni sul progetto  
  
-   Generale (conversione, migrazione, il caricamento di oggetti)  
  
-   Synchronization  
  
-   GUI  
  
-   Mapping dei tipi  
  
Include inoltre quattro modalità per la configurazione di queste impostazioni:  
  
-   Impostazione predefinita  
  
-   Optimistic  
  
-   Full  
  
-   Personalizzato  
  
La modalità predefinita è consigliata per la maggior parte degli utenti. La modalità ottimistica mantiene più la sintassi Oracle corrente e facile da leggere. Tuttavia, mantenendo la sintassi corrente potrebbe non essere accurata. Se la sintassi di Oracle deve essere convertita nell'equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informazioni sulla sintassi, la modalità completa esegue la conversione più completa, ma il codice risulta potrebbe essere più difficile da leggere. Nella modalità personalizzata, impostare le opzioni.  
  
Per altre informazioni sulle impostazioni e come vengono applicate le impostazioni in ciascuna modalità, vedere gli argomenti seguenti:  
  
-   [Le impostazioni di progetto &#40;conversione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Le impostazioni di progetto &#40;migrazione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [Le impostazioni di progetto&#40;sincronizzazione&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Le impostazioni di progetto &#40;interfaccia utente grafica&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [Le impostazioni di progetto &#40;Mapping dei tipi&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>Impostazione delle opzioni del progetto  
In SSMA, è possibile configurare le impostazioni predefinite per tutti i progetti. Queste impostazioni vengono salvate nel file di configurazione di SSMA e applicate a ogni nuovo progetto creato.  
  
**Per impostare le opzioni del progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu fare clic su **impostazioni di progetto predefinite**.  
  
2.  Nel **impostazioni di progetto predefinite** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    -   Seleziona tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati dal **versione di destinazione della migrazione** elenco a discesa fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare la conversione o Migrazione.  
  
    -   Per selezionare una modalità predefinita, il **modalità** casella di riepilogo a discesa, selezionare **predefinito**, **Optimistic**, o **completo**.  
  
    -   Per specificare le impostazioni personalizzate, selezionare o immettere le nuove impostazioni o i valori.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
È anche possibile personalizzare le impostazioni per il progetto corrente. Queste impostazioni vengono salvate nel file di progetto corrente.  
  
**Per personalizzare le impostazioni per il progetto corrente**  
  
1.  Nel **degli strumenti** dal menu fare clic su **le impostazioni del progetto**.  
  
2.  Nel **impostazioni del progetto** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    -   Per selezionare una modalità predefinita, il **modalità** casella di riepilogo a discesa, selezionare **predefinito**, **Optimistic**, o **completo**.  
  
    -   Per specificare una modalità personalizzata, nelle **modalità** , quindi selezionare **personalizzato**e quindi selezionare le impostazioni di progetto appropriato.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di Oracle e SQL Server Data Types &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   In caso contrario, è possibile convertire le definizioni degli oggetti di database Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetto. Per altre informazioni, vedere [conversione di schemi Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Mapping di tipi di dati SQL Server e Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
