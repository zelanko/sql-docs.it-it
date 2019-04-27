---
title: Usare certificati per un endpoint del mirroring del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 116c5d900cf56d89c01bbf333d2d8bd3905aa371
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754023"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>Utilizzare certificati per un endpoint del mirroring del database (Transact-SQL)
  Per abilitare l'autenticazione del certificato per il mirroring del database in una determinata istanza del server, l'amministratore di sistema deve configurare ogni istanza del server per l'utilizzo dei certificati nelle connessioni in uscita e in ingresso. Le connessioni in uscita devono essere configurate per prime.  
  
> [!NOTE]  
>  Tutte le connessioni per il mirroring in un'istanza del server utilizzano un singolo endpoint del mirroring del database ed è necessario specificare il metodo di autenticazione dell'istanza del server quando si crea l'endpoint. È pertanto possibile utilizzare un solo metodo di autenticazione per istanza di server per il mirroring del database.  
  
## <a name="configuring-outbound-connections"></a>Configurazione delle connessioni in uscita  
 Per ogni istanza del server che si sta configurando per il mirroring del database eseguire la procedura seguente:  
  
1.  Nel database **master** creare una chiave master del database.  
  
2.  Nel database **master** creare un certificato crittografato nell'istanza del server.  
  
3.  Creare un endpoint per l'istanza del server utilizzando il relativo certificato.  
  
4.  Eseguire il backup del certificato in un file e copiarlo nell'altro sistema o negli altri sistemi.  
  
 È necessario eseguire questa procedura per ogni partner e per il server di controllo del mirroring, se disponibile.  
  
 Per altre informazioni, vedere [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md).  
  
## <a name="configuring-inbound-connections"></a>Configurazione delle connessioni in ingresso  
 Eseguire quindi la procedura seguente per ogni partner che si sta configurando per il mirroring del database. Nel database **master** :  
  
1.  Creare un account di accesso per l'altro sistema.  
  
2.  Creare un utente per tale account di accesso.  
  
3.  Ottenere il certificato per l'endpoint del mirroring dell'altra istanza del server.  
  
4.  Associare il certificato all'utente creato nel passaggio 2.  
  
5.  Concedere l'autorizzazione CONNECT all'account di accesso per l'endpoint del mirroring.  
  
 Se è disponibile un server di controllo del mirroring, è necessario configurare le connessioni in ingresso anche per tale server. Questa operazione prevede la configurazione di account di accesso, utenti e certificati per il server di controllo del mirroring in entrambi i partner, e viceversa.  
  
 Per altre informazioni, vedere [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in ingresso &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md).  
  
## <a name="security"></a>Sicurezza  
 A meno che la sicurezza della rete in uso non sia già garantita, è consigliabile utilizzare la crittografia per le connessioni per il mirroring del database. Per altre informazioni, vedere [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md).  
  
 Quando si copia un certificato in un altro sistema, utilizzare un metodo di copia sicuro. È estremamente importante garantire la protezione di tutti i certificati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione della chiave master di un database](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [Sicurezza del trasporto per i gruppi di disponibilità AlwaysOn e mirroring del Database &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
  
  
