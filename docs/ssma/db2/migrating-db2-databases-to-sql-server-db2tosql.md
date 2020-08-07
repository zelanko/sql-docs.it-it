---
title: Migrazione di database DB2 a SQL Server (DB2ToSQL) | Microsoft Docs
description: Usare questa procedura consigliata per eseguire la migrazione di database DB2 a SQL Server o al database SQL di Azure usando SQL Server Migration Assistant (SSMA).
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c66e88ff81cc8f7d06d3d946be8e476b175d1b47
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823682"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrazione di database DB2 a SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) per DB2 è un ambiente completo che consente di migrare rapidamente i database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o al database SQL di Azure. Utilizzando SSMA per DB2, è possibile esaminare gli oggetti e i dati di database, valutare i database per la migrazione, eseguire la migrazione di oggetti di database al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database SQL di Azure e quindi eseguire la migrazione dei dati al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database SQL di Azure. Si noti che non è possibile eseguire la migrazione di schemi SYS e DB2 di sistema.  
  
## <a name="recommended-migration-process"></a>Processo di migrazione consigliato  
Per eseguire correttamente la migrazione di oggetti e dati da database DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database SQL di Azure, usare il processo seguente:  
  
1.  [Nuovo progetto SSMA](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Dopo aver creato il progetto, è possibile impostare le opzioni di conversione del progetto, migrazione e mapping dei tipi. Per informazioni sulle impostazioni del progetto, vedere [Impostazioni progetto &#40;conversione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) e sezioni correlate. Per informazioni su come personalizzare i mapping dei tipi di dati, vedere [mapping di tipi di dati DB2 e SQL Server &#40;&#41;DB2ToSQL ](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Connettersi al database DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Connessione a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  Eseguire il [mapping di schemi DB2 a SQL Server schemi](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Facoltativamente, i [report di valutazione](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) consentono di valutare gli oggetti di database per la conversione e stimare il tempo di conversione.  
  
6.  [Convertire gli schemi DB2](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Caricare gli oggetti di database convertiti in SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Questa operazione può essere eseguita in uno dei modi seguenti:  
  
    -   Salvare uno script ed eseguirlo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Sincronizzare gli oggetti di database.  
  
8.  [Migrazione dei dati DB2 in SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Se necessario, aggiornare le applicazioni di database.  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introduzione con SSMA per DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
