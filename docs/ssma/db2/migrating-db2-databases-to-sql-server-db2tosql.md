---
title: Database DB2 la migrazione a SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8ee6e9cca2e16a180f869df7bcec07bb7b09e390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63071147"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrazione di database DB2 a SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) per DB2 è un ambiente completo che consente di eseguire rapidamente la migrazione di database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Tramite SSMA per DB2, è possibile esaminare gli oggetti di database e i dati, valutare i database per la migrazione, eseguire la migrazione di oggetti di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, quindi eseguire la migrazione dei dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure. Si noti che è possibile eseguire la migrazione di schemi SYS e di sistema DB2.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per completare la migrazione oggetti e i dati dal database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure, procedere come segue:  
  
1.  [Nuovo progetto SSMA](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Dopo aver creato il progetto, è possibile impostare conversione del progetto, la migrazione e le opzioni di mapping dei tipi. Per informazioni sulle impostazioni del progetto, vedere [impostazioni del progetto &#40;conversione&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e relative sezioni. Per informazioni su come personalizzare i mapping dei tipi di dati, vedere [Mapping di DB2 e tipi di dati di SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Connettersi al database DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [La connessione a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Eseguire il mapping di schemi DB2 a schemi SQL Server](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Facoltativamente [report di valutazione](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) per valutare gli oggetti di database per la conversione e stimare il tempo di conversione.  
  
6.  [Conversione di schemi DB2](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    È possibile eseguire questa operazione in uno dei modi seguenti:  
  
    -   Salvare uno script ed eseguirlo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Sincronizzare gli oggetti di database.  
  
8.  [La migrazione di dati DB2 in SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Se necessario, aggiornare le applicazioni di database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introduzione a SSMA per DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
