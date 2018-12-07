---
title: Impostare un server di inoltro eventi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc60b53841cc44d094d5cea339ba2bd06f492aa6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502445"
---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>Designate an Events Forwarding Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene descritto come designare un server al quale verranno inoltrati eventi da [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eventi in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . Si noti che l'inoltro di eventi si applica agli eventi inoltrati tra server, non agli eventi inoltrati tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ospitate in un singolo computer. Notare inoltre che per ricevere eventi inoltrati, il server di gestione degli avvisi deve essere un'istanza predefinita di SQL Server.  
  
**Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
    [Security](#Security)  
  
-   **Per impostare un server di inoltro eventi utilizzando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Prima di iniziare  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Per impostare un server di inoltro eventi  
  
1.  In **Esplora oggetti** fare clic sul segno più per espandere il server da cui si desidera inoltrare gli eventi a un altro server.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent** e scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà SQL Server Agent -**_nome_server_ fare clic su **Avanzate** in **Selezione pagina**.  
  
4.  In **Inoltro eventi SQL Server**selezionare la casella di controllo **Inoltra eventi a un altro server** .  
  
5.  Nell'elenco **Server** fare clic su un server e quindi in **Eventi**selezionare una delle opzioni seguenti:  
  
    -   Selezionare **Eventi non gestiti** per inoltrare solo gli eventi che non sono stati gestiti da avvisi locali.  
  
    -   Selezionare **Tutti gli eventi** per inoltrare tutti gli eventi, indipendentemente dal fatto che siano stati gestiti o meno da avvisi locali.  
  
6.  Nell'elenco **Eventi con gravità maggiore o uguale a** selezionare il livello di gravità che contraddistingue gli eventi da inoltrare al server selezionato.  
  
7.  Al termine, fare clic su **OK**.  
  
