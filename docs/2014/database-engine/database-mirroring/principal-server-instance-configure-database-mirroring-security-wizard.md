---
title: Istanza server principale (Configurazione guidata sicurezza mirroring del database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4fde67fc6b38e81c7367ee1e298439810b0b35c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754565"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>Istanza server principale (Configurazione guidata sicurezza mirroring del database)
  Utilizzare questa pagina per specificare le informazioni relative all'istanza del server del database principale. Il database principale è la copia del database che avvia la sessione di mirroring. Dopo l'avvio della sessione il database principale è la copia del database che accetta le modifiche dell'utente. Quando si verifica un failover, i ruoli principale e mirror vengono invertiti, quindi il database principale iniziale potrebbe non rimanere tale.  
  
 **Per configurare il mirroring del database tramite SQL Server Management Studio**  
  
-   [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Avvio della Configurazione guidata sicurezza mirroring del database &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opzioni  
 **Istanza server principale**  
 Poiché il mirroring del database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] viene sempre configurato dal server principale, l'istanza corrente del server è sempre l'istanza del server principale.  
  
 **Porta di attesa**  
 Il funzionamento di questa opzione dipende dalla presenza dell'endpoint di mirroring per l'istanza del server corrente, come illustrato di seguito:  
  
-   Se non esiste una porta di attesa per l'istanza del server, nella casella di testo **Porta** verrà visualizzato il numero di porta 5022. È possibile utilizzare qualsiasi numero di porta disponibile, ad esempio 7022.  
  
-   Se l'endpoint di mirroring esiste già, viene visualizzato il numero di porta ricevuto dall'endpoint. Se è necessario modificare la porta, utilizzare un comando ALTER ENDPOINT. Per altre informazioni, vedere [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
> [!NOTE]  
>  È necessario un numero di porta.  
  
 **Nome endpoint**  
 Se l'endpoint di mirroring esiste per l'istanza del server, viene visualizzato il nome dell'endpoint. Se l'endpoint non esiste, è possibile specificare il nome dell'endpoint.  
  
 **Crittografa i dati inviati tramite questo endpoint**  
 La crittografia è abilitata per impostazione predefinita. Quando è abilitata, la crittografia non solo è supportata, ma è anche necessaria e utilizza i valori predefiniti per tutte le opzioni di crittografia. Per altre informazioni, vedere [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
 Per disabilitare la crittografia, deselezionare la casella di controllo. Per abilitare di nuovo la crittografia, selezionare la casella di controllo.  
  
## <a name="see-also"></a>Vedere anche  
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Proprietà del database &#40;Pagina Mirroring&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
