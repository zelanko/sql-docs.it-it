---
title: Impostazione delle opzioni progetto (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e397bf4480dd7a9955fb8c7acbce0d11fd910893
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215942"
---
# <a name="setting-project-options-mysqltosql"></a>Impostazione delle opzioni progetto (MySQLToSQL)
Per ogni progetto SSMA, è possibile impostare le opzioni a livello di progetto. Queste opzioni specificano come gli oggetti vengono convertiti, migrazione dei dati e come eseguire il mapping tipi di dati di origine ai tipi di dati di destinazione.  Prima di convertire gli oggetti in SQL Server o SQL Azure o eseguire la migrazione dei dati in SQL Server o SQL Azure, verificare che le opzioni di configurazione siano appropriate per il progetto.  
  
SSMA consente di configurare le opzioni predefinite per tutti i progetti. Queste opzioni vengono applicate a ogni nuovo progetto creato. È quindi possibile personalizzare le opzioni per ogni progetto.  
  
## <a name="configuration-options-and-modes"></a>Le modalità e le opzioni di configurazione  
SSMA è cinque set di impostazioni di progetto:  
  
-   Informazioni sul progetto  
  
-   Generale (conversione, migrazione e SQL Azure)  
  
-   Synchronization  
  
-   GUI  
  
-   Mapping dei tipi  
  
Le impostazioni di progetto possono essere configurate in quattro modi:  
  
-   Impostazione predefinita  
  
-   Optimistic  
  
-   Full  
  
-   Personalizzato  
  
La modalità predefinita è consigliata per la maggior parte degli utenti. La modalità ottimistica mantiene più la sintassi di MySQL corrente e facile da leggere. Tuttavia, mantenendo la sintassi corrente potrebbe non essere accurata. Se la sintassi di MySQL deve essere convertita in sintassi equivalente di SQL Server o SQL Azure, la modalità completa esegue la conversione più completa. Il codice risultante, tuttavia, potrebbe essere più difficile da leggere. Nella modalità personalizzata, è possibile impostare le opzioni.  
  
Per altre informazioni sulle impostazioni e come vengono applicate le impostazioni in ciascuna modalità, vedere gli argomenti seguenti:  
  
-   [Le impostazioni di progetto &#40;conversione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Le impostazioni di progetto &#40;migrazione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Impostazioni progetto (GUI) (SSMA comune)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Le impostazioni di progetto &#40;Mapping dei tipi&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Le impostazioni di progetto &#40;sincronizzazione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Le impostazioni di progetto &#40;Azure SQL database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Impostazione delle opzioni del progetto  
In SSMA, è possibile configurare le impostazioni predefinite per tutti i progetti. Queste impostazioni vengono salvate nel file di configurazione di SSMA e applicate a ogni nuovo progetto creato.  
  
**Per impostare le opzioni del progetto predefinito**  
  
1.  Nel **degli strumenti** dal menu fare clic su **impostazioni di progetto predefinite**.  
  
2.  Nel **impostazioni di progetto predefinite** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    1.  Seleziona tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati / modificato da **versione di destinazione della migrazione** elenco a discesa, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **Conversione o la migrazione o di SQL Azure** opzione.  
  
    2.  Per selezionare una modalità predefinita, selezionare **predefinite**, **Optimistic**, o **completo** dal **modalità** casella di riepilogo a discesa.  
  
    3.  Per specificare le impostazioni personalizzate, selezionare o immettere le nuove impostazioni o i valori.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
È anche possibile personalizzare le impostazioni per il progetto corrente. Le impostazioni di ottengano salvate nel file di progetto corrente.  
  
**Per personalizzare le impostazioni per il progetto corrente**  
  
1.  Nel **degli strumenti** menu, fare clic su **ProjectSettings**.  
  
2.  Nel **ProjectSettings** nella finestra di dialogo, utilizzare una delle procedure riportate di seguito:  
  
    1.  Per selezionare una modalità predefinita, selezionare **predefinite**, **Optimistic**, o **completo** dal **modalità** casella di riepilogo a discesa.  
  
    2.  Per specificare una modalità personalizzata, selezionare **personalizzati** dalle **modalità** casella di riepilogo a discesa. E quindi selezionare le impostazioni di progetto appropriato.  
  
3.  Fare clic su **OK** per salvare le impostazioni.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo nel processo di migrazione dipende dalle esigenze del progetto:  
  
-   Per personalizzare il mapping dei tipi di dati di origine e di destinazione, vedere [Mapping di MySQL e SQL Server Data Types &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   In caso contrario, è possibile convertire le definizioni degli oggetti di database MySQL in SQL Server o le definizioni degli oggetti di SQL Azure. Per altre informazioni, vedere [conversione di database MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Mapping di tipi di dati SQL Server e MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
