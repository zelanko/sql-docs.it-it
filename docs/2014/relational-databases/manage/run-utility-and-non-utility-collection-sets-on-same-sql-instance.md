---
title: Considerazioni per l'esecuzione di set di raccolta di utilità e non di utilità nella stessa istanza di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f34dfa48e9962e445aa8848399980331899065f1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023202"
---
# <a name="considerations-for-running-utility-and-non-utility-collection-sets-on-the-same-instance-of-sql-server"></a>Considerazioni per l'esecuzione di set di raccolta dell'utilità e non appartenenti all'utilità nella stessa istanza di SQL Server
  L'esecuzione side-by-side del set di raccolta di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dei set di raccolta non appartenenti a Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è supportata. Ciò significa che un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere monitorata da altri set di raccolta anche se l'istanza è membro di un'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È tuttavia necessario disabilitare la funzionalità della raccolta dati non appartenente all'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mentre l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene registrata nell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Dopo la registrazione dell'istanza con il punto di controllo dell'utilità, è possibile riavviare i set di raccolta non appartenenti dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tuttavia, tutti i set di raccolta sull'istanza gestita caricheranno i propri dati nel data warehouse di gestione dell'utilità (UMDW); il nome del file UMDW è sysutility_mdw.  
  
 Per eseguire side-by-side i set di raccolta dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i set di raccolta non appartenenti all'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tenere presente quanto segue:  
  
-   L'esecuzione side-by-side dei set di raccolta è supportata.  
  
-   È necessario disabilitare gli agenti di raccolta dati esistenti mentre si registrano le istanze nell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per soddisfare i requisiti della convalida, è necessario eseguire le stored procedure seguenti sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima di creare un punto di controllo dell'utilità e su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prima di registrarla nell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     Se non si eseguono queste stored procedure prima di avviare la procedura guidata Crea punto di controllo dell'utilità o Aggiungi istanza gestita, l'operazione non riuscirà.  
  
-   È necessario utilizzare il data warehouse di gestione (sysutility_mdw) dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per tutti i set di raccolta su un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md)   
 [Configurare il data warehouse del punto di controllo dell'utilità &#40;Utilità SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
