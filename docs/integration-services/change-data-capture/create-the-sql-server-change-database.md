---
description: Creare il database delle modifiche di SQL Server
title: Creare il database delle modifiche di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b49e099d675aec6158048d8a2a0fb4fe1c0ba64a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457743"
---
# <a name="create-the-sql-server-change-database"></a>Creare il database delle modifiche di SQL Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando si avvia la New Instance Wizard, viene visualizzata la pagina Create CDC Database. Utilizzare la pagina Create CDC Database per fornire informazioni sulla nuova istanza di CDC e creare un nuovo database delle modifiche.  
  
 Quando si crea un nuovo database CDC esso viene abilitato per SQL Server CDC. Questa operazione richiede un account di accesso che sia un membro del ruolo predefinito del server `sysadmin` .  
  
 Se l'utente che avvia la procedura guidata Create an Oracle CDC Instance non è un membro del ruolo predefinito del server `sysadmin` , viene visualizzata la finestra di dialogo Connect to SQL Server e vengono richieste le credenziali per un membro del ruolo sysadmin per eseguire l'attività SQL Server CDC. Quando viene creato il database CDC, l'account di accesso `sysadmin` viene eliminato e viene ripreso l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] originale utilizzato al momento dell'accesso a Oracle Designer Console.  
  
> [!IMPORTANT]  
>  Per attività diverse dall'abilitazione del database per SQL Server CDC, l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato per l'esecuzione della Procedura guidata nuova istanza deve disporre delle autorizzazioni UPDATE e del ruolo predefinito del server `dbcreator` per il database MSXDBCDC.  
  
 Per informazioni sull'immissione dei dati nella finestra di dialogo Connect to SQL Server, vedere [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>Opzioni  
 **Oracle CDC Instance**  
 Specificare le informazioni seguenti sull'istanza di CDC che si desidera creare.  
  
-   **Name**: digitare un nome per il nuovo servizio. Sarà anche il nome del nuovo database delle modifiche.  
  
-   **Description**: digitare una descrizione per la nuova istanza che consenta di identificarla. Operazione facoltativa.  
  
 **SQL Server Change Database**  
 Questa sezione viene utilizzata per creare il database.  
  
1.  **Change Database**: nome del nuovo database delle modifiche. Il nome del database equivale al nome specificato per l'istanza. In questo campo di sola lettura viene visualizzato il percorso completo del database.  
  
2.  **Create Database**: fare clic su **Create Database** per creare il database.  
  
     Per creare il database, l'account di accesso deve disporre del ruolo del server `sysasmin` . Per ulteriori informazioni, vedere la nota sulla sicurezza.  
  
     Dopo avere creato il database, è possibile fare clic su **Next** in [Connect to an Oracle Source Database](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Servizio Oracle CDC](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
