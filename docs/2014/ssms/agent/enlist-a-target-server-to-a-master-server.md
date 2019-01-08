---
title: Integrare un server di destinazione in un server master | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3d0d91de95e82fcd174aa9290e208afda5bef91
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786213"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Integrare un server di destinazione in un server master
  In questo argomento viene illustrata la procedura per l'aggiunta di server di destinazione a una configurazione di amministrazione multiserver. Eseguire questa procedura dal server master. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects (SMO).  
  
 Per informazioni sugli effetti dell'uso dell'account di Windows per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent su un ambiente multiserver, vedere [Creazione di un ambiente multiserver](create-a-multiserver-environment.md).  
  
 Per impostazione predefinita, per le connessioni tra server master e server di destinazione sono attive la crittografia SSL (Secure Sockets Layer) completa e la convalida del certificato. Per altre informazioni, vedere [Impostazione delle opzioni di crittografia nei server di destinazione](set-encryption-options-on-target-servers.md).  
  
 **Contenuto dell'argomento**  
  
-   **Per integrare un server di destinazione tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  In **Esplora oggetti**espandere un server configurato come server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Aggiungi server di destinazione**.  
  
3.  In Configurazione guidata server di destinazione, eseguire i passaggi necessari per completare la procedura.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  Utilizzare la stored procedure `sp_msx_enlist`.  Per altre informazioni, vedere [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> Usando SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione automatizzata in un'organizzazione](automated-administration-across-an-enterprise.md)  
  
  
