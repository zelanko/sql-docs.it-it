---
title: Impostare l'intervallo di polling per i server di destinazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1578bbefc9ae17baae56799d943e5ae6186628ea
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818683"
---
# <a name="set-the-polling-interval-for-target-servers"></a>Impostare l'intervallo di polling per i server di destinazione
  In questo argomento viene illustrato come impostare la frequenza utilizzata da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'aggiornamento delle informazioni dal server master ai server di destinazione. Un processo è una serie specificata di azioni eseguite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Un processo multiserver è un processo eseguito da un server master in uno o più server di destinazione.  
  
-   **Prima di iniziare:**  [Sicurezza](#Security)  
  
-   **Per impostare l'intervallo di polling per i server di destinazione usando:**  [SQL Server Management Studio](#SSMS), [Transact-SQL](#TSQL)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Ogni server di destinazione può eseguire contemporaneamente una sola istanza dello stesso processo. Ogni server di destinazione esegue periodicamente il polling del server master, scarica una copia dei nuovi processi assegnati al server di destinazione, quindi si disconnette. Il server di destinazione esegue il processo in locale, quindi si riconnette al server master per caricare lo stato del risultato del processo una volta terminato.  
  
> [!NOTE]  
>  Se il server master non è accessibile quando il server di destinazione tenta di caricare lo stato del processo, per tale stato viene eseguito lo spooling fino a quando non è possibile accedere al server master.  
  
###  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) e [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
##  <a name="SSMS"></a> Utilizzo di SQL Server Management Studio  
 **Per impostare l'intervallo di polling per i server di destinazione**  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere tale istanza.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Gestione server di destinazione**.  
  
3.  Nella scheda **Stato server di destinazione** fare clic su **Invia istruzioni**.  
  
4.  Nell'elenco **Tipo istruzione** selezionare **Imposta intervallo di polling**.  
  
5.  Nella casella **Intervallo di polling** immettere un numero di secondi compreso tra 10 e 28.800 per indicare l'intervallo di esecuzione del polling dal server di destinazione al server master.  
  
6.  In **Destinatari**eseguire una delle operazioni seguenti:  
  
    1.  Fare clic su **Tutti i server di destinazione** se tutti i server di destinazione condividono lo stesso intervallo di polling.  
  
    2.  Fare clic su **Solo i server di destinazione seguenti** se non tutti i server di destinazione condividono lo stesso intervallo di polling e quindi selezionare ogni server di destinazione che utilizzerà l'intervallo specifico.  
  
##  <a name="TSQL"></a> Utilizzo di Transact-SQL  
 **Per impostare l'intervallo di polling per i server di destinazione**  
  
1.  In Esplora oggetti connettersi a un'istanza del motore di database ed espanderla.  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra di query, usare il [sp_post_msx_operation &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql) stored procedure per impostare l'intervallo di polling per i server di destinazione di sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [dbo.sysdownloadlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysdownloadlist-transact-sql)  
  
  
