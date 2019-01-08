---
title: Modifica l'Account Proxy per la raccolta dell'utilità è impostato su un'istanza gestita di SQL Server (utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: efa4af0c12379abaab2d810fd39ce6d7a3b0afef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782313"
---
# <a name="change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server-sql-server-utility"></a>Modificare l'account proxy per il set di raccolta dell'utilità in un'istanza gestita di SQL Server (Utilità SQL Server)
  In questo argomento viene descritto come modificare l'account proxy per il set di raccolta utilità in un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>Per modificare l'account proxy per il set di raccolta dell'utilità in un'istanza gestita di SQL Server  
  
1.  Rimuovere l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   In **Esplora utilità** in SSMS fare clic sul nodo **Istanze gestite** .  
  
    -   Nella visualizzazione elenco di **Esplora utilità** fare clic con il pulsante destro del mouse sul nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e scegliere **Rimuovi istanza gestita**. Per altre informazioni, vedere [Rimuovere un'istanza di SQL Server da Utilità SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
2.  Registrare nuovamente l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   In **Esplora utilità** in SSMS fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** e scegliere **Aggiungi istanza gestita**.  
  
    -   Seguire le istruzioni nelle finestre visualizzate per completare la procedura guidata, specificando il nuovo account proxy.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](sql-server-utility-features-and-tasks.md)   
 [Attività e funzionalità di Utilità SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
