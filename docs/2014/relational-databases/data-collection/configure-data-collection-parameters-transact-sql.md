---
title: Configurare i parametri per la raccolta dati (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a8333b47612b4fbd933ef132e886b8125ffb58a3
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970521"
---
# <a name="configure-data-collection-parameters-transact-sql"></a>Configurazione dei parametri per la raccolta dati (Transact-SQL)
  Prima di creare un set di raccolta personalizzato è necessario configurare i parametri della raccolta dati. A tale scopo, utilizzare le stored procedure fornite con l'agente di raccolta dati. Il completamento di questa attività comporta l'utilizzo dell'editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per effettuare la procedura descritta di seguito.  
  
> [!NOTE]  
>  I parametri per la raccolta dati possono essere configurati una volta sola. Dopo la configurazione, tali parametri vengono utilizzati per qualsiasi set di raccolta aggiuntivo creato.  
  
### <a name="configure-data-collection-parameters"></a>Configurazione dei parametri per la raccolta dati  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al database in cui si desidera creare un set di raccolta personalizzato.  
  
2.  Nell'editor di query eseguire le istruzioni indicate di seguito.  
  
    ```sql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](data-collection.md)   
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  
