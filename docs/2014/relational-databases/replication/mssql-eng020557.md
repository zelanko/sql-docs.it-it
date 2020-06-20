---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 12bbdf4c7cca974953602f760c2d298424eaaa8a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010275"
---
# <a name="mssql_eng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|20557|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Arresto dell'agente. Per ulteriori informazioni, cercare nella cronologia dei processi di SQL Server Agent il processo '%s'.|  
  
## <a name="explanation"></a>Spiegazione  
 Un agente di replica è stato arrestato ma nella tabella di cronologia appropriata non è stato scritto nessun motivo oppure l'agente è stato arrestato durante l'esecuzione di un processo.  
  
## <a name="user-action"></a>Azione dell'utente  
  
-   Riavviare l'agente per verificare se viene eseguito senza errori. Per altre informazioni, vedere [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Concetti di base relativi ai file eseguibili dell'agente di replica](concepts/replication-agent-executables-concepts.md).  
  
-   Verificare nella cronologia dell'agente e nella cronologia processo la presenza di eventuali altri errori verificatisi nello stesso momento. Per informazioni sui dettagli di stato e di errore dell'agente di visualizzazione in Monitoraggio replica, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](monitor/view-information-and-perform-tasks-replication-monitor.md).
-   Verificare il funzionamento della connettività di base tra i computer a cui l'agente accede e quindi connettersi a ogni computer usando un'utilità, ad esempio **sqlcmd** . Per la connessione utilizzare lo stesso account con cui l'agente effettua le connessioni. Per ulteriori informazioni sulle autorizzazioni necessarie per ogni account di agente, vedere [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Se l'errore si verifica durante la creazione o l'applicazione di uno snapshot, verificare l'eventuale presenza di errori nei file della directory snapshot.  
  
-   Se l'errore continua a verificarsi, aumentare il livello di dettaglio per la registrazione delle operazioni dell'agente e specificare un file di output per il log. A seconda del contesto dell'errore, in questo modo è possibile ottenere ulteriori informazioni sui passaggi che conducono all'errore e messaggi di errore aggiuntivi. Per ulteriori informazioni sulla configurazione della registrazione per la replica, vedere l'articolo [312292](https://support.microsoft.com/kb/312292)della Microsoft Knowledge Base.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
