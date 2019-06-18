---
title: Disabilitare i vincoli di chiave esterna per la replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fafc1fc122576bd8432ba76a34dbee001989421d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62515737"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>Disabilitare i vincoli di chiave esterna per la replica
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  È possibile disabilitare vincoli di chiave esterna per la replica in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Questa operazione può essere utile se si pubblicano dati da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Se una tabella viene pubblicata usando la replica, i vincoli di chiave esterna vengono disabilitati automaticamente per le operazioni eseguite dagli agenti di replica. Quando un agente di replica esegue un accodamento, aggiornamento o una eliminazione a un sottoscrittore, il vincolo non viene controllato; se invece un utente esegue un accodamento, un aggiornamento o una eliminazione, il vincolo viene controllato. Il vincolo viene disabilitato per l'agente di replica in quanto esso è già stato controllato nel server di pubblicazione quando i dati sono stati inseriti, aggiornati o eliminati.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per disabilitare un vincolo di chiave esterna per la replica usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Per disabilitare un vincolo di chiave esterna per la replica  
  
1.  In **Esplora oggetti**espandere la tabella contenente il vincolo di chiave esterna che si desidera modificare, quindi espandere la cartella **Chiavi** .  
  
2.  Fare clic con il pulsante destro del mouse sul vincolo di chiave esterna e selezionare **Modifica**.  
  
3.  Nella finestra di dialogo **Relazioni chiavi esterne** scegliere **No** per **Attiva per replica**.  
  
4.  Scegliere **Chiudi**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Per disabilitare un vincolo di chiave esterna per la replica  
  
1.  Per eseguire questa attività in [!INCLUDE[tsql](../../includes/tsql-md.md)], rimuovere il vincolo della chiave esterna. Successivamente aggiungere un nuovo vincolo della chiave esterna e specificare l'opzione NOT FOR REPLICATION.  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
