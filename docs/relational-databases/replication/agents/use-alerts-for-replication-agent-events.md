---
description: Utilizzare gli avvisi per gli eventi degli agenti di replica
title: Usare gli avvisi per gli eventi degli agenti di replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d0fbec0a8ff1bcd6416ab0c24166a5bf5559cb8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428043"
---
# <a name="use-alerts-for-replication-agent-events"></a>Utilizzare gli avvisi per gli eventi degli agenti di replica
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent consentono di monitorare gli eventi, ad esempio quelli dell'agente di replica, tramite avvisi. Utilizzando[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent è possibile monitorare il registro applicazioni di Windows per rilevare gli eventi associati ad avvisi. Se si verifica un evento di questo tipo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent risponde automaticamente eseguendo un'attività definita dall'utente e/o inviando un messaggio di posta elettronica o tramite cercapersone a un operatore specificato. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include un set di avvisi predefiniti per gli agenti di replica che è possibile configurare per l'esecuzione di un'attività e/o la notifica di un operatore. Per ulteriori informazioni sulla definizione di un'attività da eseguire, vedere la sezione "Risposte automatiche a un avviso" in questo argomento.  
  
 Quando un computer viene configurato come server di distribuzione, vengono installati gli avvisi seguenti:  
  
|ID del messaggio|Avviso predefinito|Condizione che genera l'avviso|Inserimento di informazioni aggiuntive in msdb..sysreplicationalerts|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**Replica: operazione dell'agente riuscita**|La chiusura dell'agente è stata completata correttamente.|Sì|  
|14151|**Replica: errore dell'agente**|Si è verificato un errore durante la chiusura dell'agente.|Sì|  
|14152|**Replica: nuovo tentativo dell'agente**|La chiusura dell'agente avviene in seguito al tentativo non riuscito di ripetere un'operazione. In questo caso, l'agente rileva un errore quale la non disponibilità del server, un deadlock, un errore di connessione o un errore di timeout.|Sì|  
|14157|**Replica: eliminata sottoscrizione scaduta**|La sottoscrizione scaduta è stata eliminata.|No|  
|20572|**Replica: la sottoscrizione è stata reinizializzata dopo l'errore di convalida**|Il processo di risposta "Reinizializzazione delle sottoscrizioni con errori di convalida dei dati" reinizializza una sottoscrizione correttamente.|No|  
|20574|**Replica: la convalida dei dati nel Sottoscrittore non è riuscita**|La convalida dei dati dell'agente di distribuzione o di merge non è riuscita.|Sì|  
|20575|**Replica: la convalida dei dati nel Sottoscrittore è riuscita**|La convalida dei dati dell'agente di distribuzione o di merge ha avuto esito positivo.|Sì|  
|20578|**Replica: arresto dell'agente personalizzato**|||  
|22815|**Avviso di rilevamento dei conflitti peer-to-peer**|L'agente di distribuzione ha rilevato un conflitto durante il tentativo di applicare una modifica a un nodo peer-to-peer.|Sì|  
  
 In aggiunta a questi avvisi, in Monitoraggio replica è disponibile un set di avvisi relativi allo stato e alle prestazioni. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). È inoltre possibile definire avvisi per altri eventi di replica utilizzando l'infrastruttura degli avvisi di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Creare un evento definito dall'utente](https://msdn.microsoft.com/library/03d71a35-97fa-4bba-aa9a-23ac9c9cf879).  
  
 **Per configurare gli avvisi predefiniti della replica**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Configurare gli avvisi di replica predefiniti &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>Visualizzazione diretta del registro applicazioni  
 Per visualizzare il registro applicazioni di Windows, utilizzare il Visualizzatore eventi di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Il registro applicazioni contiene messaggi di errore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nonché messaggi per molte altre attività eseguite nel computer. Diversamente dal log degli errori di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a ogni avvio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non viene creato un nuovo registro applicazioni (durante ogni sessione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono scritti nuovi eventi in un registro applicazioni esistente). È tuttavia possibile specificare il periodo di memorizzazione degli eventi registrati. Quando si visualizza il registro applicazioni di Windows, è possibile filtrarlo per eventi specifici. Per ulteriori informazioni, vedere la documentazione di Windows.  
  
## <a name="automating-a-response-to-an-alert"></a>Risposte automatiche a un avviso  
 La replica include un processo di risposta per le sottoscrizioni con errore di convalida dei dati nonché una struttura per la creazione di ulteriori risposte automatiche agli avvisi. Il processo di risposta si chiama **Reinizializzazione delle sottoscrizioni con errori di convalida dei dati** ed è memorizzato nella cartella [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Processi **di** Agent in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sull'abilitazione di questo processo di risposta, vedere [Configurare gli avvisi di replica predefiniti &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Se la convalida degli articoli di una pubblicazione transazionale non riesce, il processo di risposta reinizializza solo gli articoli con errore. Se la convalida degli articoli di una pubblicazione di tipo merge non riesce, il processo di risposta reinizializza tutti gli articoli della pubblicazione.  
  
### <a name="framework-for-automating-responses"></a>Struttura per le risposte automatiche  
 Quando viene generato un avviso, le informazioni necessarie per comprenderne le causa e determinare l'intervento appropriato in genere sono contenute nel messaggio di avviso stesso. L'analisi di queste informazioni può essere soggetta a errori e richiedere tempi lunghi. La replica semplifica l'automatizzazione delle risposte grazie alla specifica di informazioni aggiuntive sull'avviso nella tabella di sistema **sysreplicationalerts** . Le informazioni fornite sono già analizzate in un formato facilmente utilizzabile in programmi personalizzati.  
  
 Se, ad esempio, i dati della tabella **Sales.SalesOrderHeader** nel Sottoscrittore A non vengono convalidati, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene attivato il messaggio di avviso 20574 per avvisare l'utente dell'errore. Il messaggio visualizzato sarà il seguente: "La sottoscrizione del Sottoscrittore 'A' dell'articolo 'SalesOrderHeader' della pubblicazione 'MyPublication' non ha superato la convalida dei dati".  
  
 Se si crea una risposta in base al messaggio, è necessario analizzare in modo manuale il nome del Sottoscrittore, il nome dell'articolo, il nome della pubblicazione e l'errore indicato nel messaggio. Poiché, tuttavia, l'agente di distribuzione e l'agente di merge scrivono le stesse informazioni nella tabella di sistema **sysreplicationalerts** , il processo di risposta può ricavare le informazioni appropriate direttamente dalla tabella, insieme a dettagli quali il tipo di agente, l'ora di attivazione dell'avviso, il database di pubblicazione, il database del Sottoscrittore e il tipo di pubblicazione. Sebbene non sia possibile associare la riga esatta a un'istanza specifica dell'avviso, la tabella include una colonna **status** che consente di tenere traccia delle voci elaborate. Le voci di questa tabella sono disponibili per l'intero periodo di memorizzazione della cronologia.  
  
 Se, ad esempio, si desidera creare un processo di risposta in [!INCLUDE[tsql](../../../includes/tsql-md.md)] che elabori il messaggio di avviso 20574, è possibile utilizzare la logica seguente:  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione dell'agente di replica](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Monitoraggio &#40;replica&#41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
