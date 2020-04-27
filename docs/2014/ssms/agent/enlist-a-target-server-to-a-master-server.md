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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211398"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Integrare un server di destinazione in un server master
  In questo argomento viene illustrata la procedura per l'aggiunta di server di destinazione a una configurazione di amministrazione multiserver. Eseguire questa procedura dal server master. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects (SMO).  
  
 Per informazioni sugli effetti dell'uso dell'account di Windows per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent su un ambiente multiserver, vedere [Creazione di un ambiente multiserver](create-a-multiserver-environment.md).  
  
 Per impostazione predefinita, per le connessioni tra server master e server di destinazione sono attive la crittografia SSL (Secure Sockets Layer) completa e la convalida del certificato. Per altre informazioni, vedere [Impostazione delle opzioni di crittografia nei server di destinazione](set-encryption-options-on-target-servers.md).  
  
 **Contenuto dell'articolo**  
  
-   **Per integrare un server di destinazione tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  In **Esplora oggetti**espandere un server configurato come server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Aggiungi server di destinazione**.  
  
3.  In Configurazione guidata server di destinazione, eseguire i passaggi necessari per completare la procedura.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Per integrare un server di destinazione  
  
1.  Utilizzare la stored procedure `sp_msx_enlist`.  Per ulteriori informazioni, vedere [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>Utilizzo di SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>Vedi anche  
 [Amministrazione automatizzata in un'organizzazione](automated-administration-across-an-enterprise.md)  
  
  
