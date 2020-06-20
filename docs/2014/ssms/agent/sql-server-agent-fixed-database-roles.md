---
title: Ruoli di database predefiniti di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: stevestein
ms.author: sstein
ms.openlocfilehash: e5e523f720292909ccb9d943524e5d6d7d017b28
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058746"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Ruoli di database predefiniti di SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha a disposizione i seguenti ruoli predefiniti del database **msdb**, che consentono agli amministratori di controllare in modo più capillare l'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Sono previsti i seguenti ruoli, elencati a partire da quello che ha meno privilegi:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Quando gli utenti che non sono membri di questi ruoli sono connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], il nodo di **SQL Server Agent** non è visibile in Esplora oggetti. Per poter usare **Agent, un utente deve essere membro di uno di questi ruoli di database predefiniti o membro del ruolo di server predefinito** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Autorizzazioni dei ruoli di database predefiniti SQL Server Agent  
 Le autorizzazioni dei ruoli di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sono concentriche le une rispetto alle altre: i ruoli con privilegi di livello più alto ereditano le autorizzazioni dei ruoli con privilegi di livello più basso in oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (compresi avvisi, operatori, processi, pianificazioni e proxy). Se ad esempio ai membri del ruolo **SQLAgentUserRole** con privilegi di livello basso è stato concesso l'accesso a proxy_A, i membri di entrambi i ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** hanno automaticamente accesso a questo proxy anche se l'accesso al proxy_A non è stato esplicitamente concesso. Ciò può avere implicazioni a livello di sicurezza e nelle sezioni seguenti verranno esaminate queste implicazioni ruolo per ruolo.  
  
### <a name="sqlagentuserrole-permissions"></a>Autorizzazioni per SQLAgentUserRole  
 **SQLAgentUserRole** è il ruolo di database predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con privilegi di livello più basso. Dispone di autorizzazioni solo su operatori, processi locali e pianificazioni di processi. I membri del ruolo **SQLAgentUserRole** hanno autorizzazioni solo sui processi locali e le pianificazioni di processo di cui sono proprietari. Essi non possono utilizzare processi multiserver (processi per server master e di destinazione) e non possono modificare la proprietà dei processi per ottenere l'accesso a processi di cui non sono già proprietari. I membri del ruolo**SQLAgentUserRole** possono visualizzare l'elenco dei proxy disponibili solo nella finestra di dialogo **Proprietà passaggio processo** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Ai membri del ruolo **SQLAgentUserRole** è visibile solo il nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Processi **in Esplora oggetti di**.  
  
> [!IMPORTANT]  
>  Prendere in considerazione le implicazioni di sicurezza prima di concedere l'accesso proxy ai **membri del** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaseroles**. I ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** sono automaticamente membri del ruolo **SQLAgentUserRole**. Ciò significa che i membri dei ruoli **SQLAgentReaderRole** e **SQLAgentOperatorRole** hanno accesso a tutti i proxy [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** e possono usare questi proxy.  
  
 Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentUserRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Operatori|Processi locali<br /><br /> (solo processi di proprietà)|Pianificazioni di processi<br /><br /> (solo pianificazioni di proprietà)|Proxy|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|Creazione/modifica/eliminazione|No|Sì <sup>1</sup>|Sì|No|  
|Visualizzazione di un elenco (enumerazione)|Sì <sup>2</sup>|Sì|Sì|Sì <sup>3</sup>|  
|Abilitazione/disabilitazione|No|Sì|Sì|Non applicabile|  
|Visualizzazione di proprietà|No|Sì|Sì|No|  
|Esecuzione/arresto/avvio|Non applicabile|Sì|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|No <sup>4</sup>|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Sì|Non applicabile|  
  
 <sup>1</sup> non è possibile modificare la proprietà del processo.  
  
 <sup>2</sup> è possibile ottenere l'elenco degli operatori disponibili da utilizzare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.  
  
 <sup>3</sup> l'elenco dei proxy è disponibile solo nella finestra di dialogo **Proprietà passaggio processo** di Management Studio.  
  
 <sup>4</sup> ai membri di **SQLAgentUserRole** deve essere concessa in modo esplicito l'autorizzazione Execute per **sp_purge_jobhistory** eliminare la cronologia processo nei processi di cui sono proprietari. I membri di tale ruolo non possono eliminare la cronologia di altri processi.  
  
### <a name="sqlagentreaderrole-permissions"></a>Autorizzazioni per SQLAgentReaderRole  
 Il ruolo**SQLAgentReaderRole** include tutte le autorizzazioni per **SQLAgentUserRole** e le autorizzazioni per visualizzare l'elenco dei processi multiserver disponibili, le loro proprietà e la loro cronologia. I membri di questo ruolo possono visualizzare non solo i processi e le pianificazioni di processo di cui sono proprietari ma anche l'elenco di tutti i processi, le pianificazioni di processo e le relative proprietà. I membri del ruolo**SQLAgentReaderRole** non possono modificare la proprietà dei processi per ottenere accesso a processi di cui non sono già proprietari. In Esplora oggetti di **i membri del ruolo** SQLAgentReaderRole [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] possono vedere solo il nodo **Processi**.  
  
> [!IMPORTANT]  
>  Prendere in considerazione le implicazioni di sicurezza prima di concedere l'accesso proxy ai **membri del** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaseroles**. I membri del ruolo **SQLAgentReaderRole** sono automaticamente membri del ruolo **SQLAgentUserRole**. Ciò significa che i membri del ruolo **SQLAgentReaderRole** hanno accesso a tutti i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** e possono usare questi proxy.  
  
 Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentReaderRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Operatori|Processi locali|Processi multiserver|Pianificazioni di processi|Proxy|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Creazione/modifica/eliminazione|No|Sì <sup>1</sup> (solo processi di proprietà)|No|Sì (solo pianificazioni di proprietà)|No|  
|Visualizzazione di un elenco (enumerazione)|Sì <sup>2</sup>|Sì|Sì|Sì|Sì <sup>3</sup>|  
|Abilitazione/disabilitazione|No|Sì (solo processi di proprietà)|No|Sì (solo pianificazioni di proprietà)|Non applicabile|  
|Visualizzazione di proprietà|No|Sì|Sì|Sì|No|  
|Modifica di proprietà|No|Sì (solo processi di proprietà)|No|Sì (solo pianificazioni di proprietà)|No|  
|Esecuzione/arresto/avvio|Non applicabile|Sì (solo processi di proprietà)|No|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Sì|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|No <sup>4</sup>|No|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Non applicabile|Sì (solo pianificazioni di proprietà)|Non applicabile|  
  
 <sup>1</sup> non è possibile modificare la proprietà del processo.  
  
 <sup>2</sup> è possibile ottenere l'elenco degli operatori disponibili da utilizzare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.  
  
 <sup>3</sup> l'elenco dei proxy è disponibile solo nella finestra di dialogo **Proprietà passaggio processo** di Management Studio.  
  
 <sup>4</sup> ai membri di **SQLAgentReaderRole** deve essere concessa in modo esplicito l'autorizzazione Execute per **sp_purge_jobhistory** eliminare la cronologia processo nei processi di cui sono proprietari. I membri di tale ruolo non possono eliminare la cronologia di altri processi.  
  
### <a name="sqlagentoperatorrole-permissions"></a>Autorizzazioni per SQLAgentOperatorRole  
 **SQLAgentOperatorRole** è il ruolo di database predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con privilegi di livello più alto. E include tutte le autorizzazioni dei ruoli **SQLAgentUserRole** e **SQLAgentReaderRole**. I membri di questo ruolo possono inoltre visualizzare proprietà di operatori e proxy e possono enumerare i proxy e gli avvisi disponibili sul server.  
  
 I membri del ruolo**SQLAgentOperatorRole** hanno autorizzazioni aggiuntive su pianificazioni e processi locali. Possono eseguire, arrestare o avviare tutti i processi locali e possono eliminare la cronologia processo di qualsiasi processo locale del server. Possono inoltre attivare o disabilitare tutte le pianificazioni e i processi locali del server. Per abilitare o disabilitare processi locali o pianificazioni, i membri di questo ruolo devono usare le stored procedure **sp_update_job** e **sp_update_schedule**. I membri di **SQLAgentOperatorRole**possono specificare solo i parametri che specificano il nome del processo o della pianificazione o l'identificatore e il parametro ** \@ Enabled** . Se si specifica un qualsiasi altro parametro, l'esecuzione di queste stored procedure non viene portata a termine. I membri del ruolo**SQLAgentOperatorRole** non possono modificare la proprietà dei processi per ottenere l'accesso a processi di cui non sono già proprietari.  
  
 I nodi **Processi**, **Avvisi**, **Operatori**e **Proxy** inclusi in Esplora oggetti di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono visibili a membri del ruolo **SQLAgentOperatorRole**. Solo il nodo **Log degli errori** non è visibile ai membri di questo ruolo.  
  
> [!IMPORTANT]  
>  Prendere in considerazione le implicazioni di sicurezza prima di concedere l'accesso proxy ai **membri del** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Agentdatabaseroles**. I membri del ruolo **SQLAgentOperatorRole** sono automaticamente membri dei ruoli **SQLAgentUserRole** e **SQLAgentReaderRole**. Ciò significa che i membri del ruolo **SQLAgentOperatorRole** hanno accesso a tutti i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che sono stati concessi al ruolo **SQLAgentUserRole** o **SQLAgentReaderRole** e possono usare questi proxy.  
  
 Nella tabella seguente vengono riepilogate le autorizzazioni per il ruolo **SQLAgentOperatorRole** su oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Azione|Avvisi|Operatori|Processi locali|Processi multiserver|Pianificazioni di processi|Proxy|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Creazione/modifica/eliminazione|No|No|Sì <sup>2</sup> (solo processi di proprietà)|No|Sì (solo pianificazioni di proprietà)|No|  
|Visualizzazione di un elenco (enumerazione)|Sì|Sì <sup>1</sup>|Sì|Sì|Sì|Sì|  
|Abilitazione/disabilitazione|No|No|Sì <sup>3</sup>|No|Sì <sup>4</sup>|Non applicabile|  
|Visualizzazione di proprietà|Sì|Sì|Sì|Sì|Sì|Sì|  
|Modifica di proprietà|No|No|Sì (solo processi di proprietà)|No|Sì (solo pianificazioni di proprietà)|No|  
|Esecuzione/arresto/avvio|Non applicabile|Non applicabile|Sì|No|Non applicabile|Non applicabile|  
|Visualizzazione cronologia processo|Non applicabile|Non applicabile|Sì|Sì|Non applicabile|Non applicabile|  
|Eliminazione cronologia processo|Non applicabile|Non applicabile|Sì|No|Non applicabile|Non applicabile|  
|Collegamento/scollegamento|Non applicabile|Non applicabile|Non applicabile|Non applicabile|Sì (solo pianificazioni di proprietà)|Non applicabile|  
  
 <sup>1</sup> è possibile ottenere l'elenco degli operatori disponibili da utilizzare in **sp_notify_operator** e nella finestra di dialogo **Proprietà processo** di Management Studio.  
  
 <sup>2</sup> non è possibile modificare la proprietà del processo.  
  
 <sup>3</sup> i membri di **SQLAgentOperatorRole** possono abilitare o disabilitare i processi locali di cui non sono proprietari usando il stored procedure **sp_update_job** e specificando i valori per i parametri ** \@ Enabled** e ** \@ job_id** (o ** \@ job_name**). Se un membro di questo ruolo specifica un qualsiasi altro parametro per questa stored procedure, la sua esecuzione non viene portata a termine.  
  
 <sup>4</sup> i membri **SQLAgentOperatorRole** possono abilitare o disabilitare le pianificazioni di cui non sono proprietari usando il stored procedure **sp_update_schedule** e specificando i valori per i parametri ** \@ Enabled** e ** \@ schedule_id** (o ** \@ Name**). Se un membro di questo ruolo specifica un qualsiasi altro parametro per questa stored procedure, la sua esecuzione non viene portata a termine.  
  
## <a name="assigning-users-multiple-roles"></a>Assegnazione di più ruoli a utenti  
 I membri del ruolo predefinito del server **sysadmin** dispongono di accesso a tutte le funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se un utente non è membro del ruolo **sysadmin** ma è membro di più di un ruolo predefinito di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, è importante tenere presente il modello ad autorizzazioni concentriche di questi ruoli. Poiché i ruoli con privilegi di livello più alto comprendono sempre tutte le autorizzazioni dei ruoli con privilegi di livello più basso, a un utente che è membro di più di un ruolo vengono concesse automaticamente le autorizzazioni associate al ruolo con privilegi di livello più alto di cui questo utente è membro.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementare SQL Server Agent sicurezza](implement-sql-server-agent-security.md)   
 [sp_update_job &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [sp_update_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [sp_notify_operator &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
