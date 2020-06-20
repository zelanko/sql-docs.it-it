---
title: Ruoli di Integration Services (servizio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 84f2a00b7376ae8869cafa36f8a4ab30d74fda19
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963919"
---
# <a name="integration-services-roles-ssis-service"></a>Ruoli Integration Services (servizio SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]include i tre ruoli predefiniti a livello di database, `db_ssisadmin` , **db_ssisltduser**e **db_ssisoperator**, per il controllo dell'accesso ai pacchetti. I ruoli possono essere implementati solo nei pacchetti salvati `msdb` nel database in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I ruoli vengono assegnati a un pacchetto in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Le assegnazioni di ruolo vengono salvate nel `msdb` database.  
  
## <a name="read-and-write-actions"></a>Azioni di lettura e scrittura  
 La tabella seguente descrive le azioni di lettura e scrittura di Windows e i ruoli predefiniti del database in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Ruolo|Azione di lettura|Azione di scrittura|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> oppure<br /><br /> `sysadmin`|Enumerazione dei propri pacchetti.<br /><br /> Enumerazione di tutti i pacchetti.<br /><br /> Visualizzazione dei propri pacchetti.<br /><br /> Visualizzazione di tutti i pacchetti.<br /><br /> Esecuzione dei propri pacchetti.<br /><br /> Esecuzione di tutti i pacchetti.<br /><br /> Esportazione dei propri pacchetti.<br /><br /> Esportazione di tutti i pacchetti.<br /><br /> Esecuzione di tutti i pacchetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Importazione di pacchetti.<br /><br /> Eliminazione dei propri pacchetti.<br /><br /> Eliminazione di tutti i pacchetti.<br /><br /> Modifica dei propri ruoli di pacchetto.<br /><br /> Modifica di tutti i ruoli di pacchetto.<br /><br /> <br /><br /> I membri ** \* \* \* importanti \* ** del ruolo db_ssisadmin e il ruolo dc_admin potrebbero essere in grado di elevare i propri privilegi a sysadmin. Questa elevazione dei privilegi può verificarsi perché tali ruoli possono modificare i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possono essere eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando il contesto di sicurezza sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per impedire questa elevazione dei privilegi durante l'esecuzione dei piani di manutenzione, set di raccolta dati e altri pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configurare i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che eseguono pacchetti in modo da utilizzare un account proxy con privilegi limitati o aggiungere solo i membri sysadmin ai ruoli db_ssisadmin e dc_admin.|  
|**db_ssisltduser**|Enumerazione dei propri pacchetti.<br /><br /> Enumerazione di tutti i pacchetti.<br /><br /> Visualizzazione dei propri pacchetti.<br /><br /> Esecuzione dei propri pacchetti.<br /><br /> Esportazione dei propri pacchetti.|Importazione di pacchetti.<br /><br /> Eliminazione dei propri pacchetti.<br /><br /> Modifica dei propri ruoli di pacchetto.|  
|**db_ssisoperator**|Enumerazione di tutti i pacchetti.<br /><br /> Visualizzazione di tutti i pacchetti.<br /><br /> Esecuzione di tutti i pacchetti.<br /><br /> Esportazione di tutti i pacchetti.<br /><br /> Esecuzione di tutti i pacchetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|nessuno|  
|**Amministratori di Windows**|Visualizzazione delle informazioni di esecuzione di tutti i pacchetti in esecuzione.|Arresto di tutti i pacchetti in esecuzione.|  
  
## <a name="sysssispackages-table"></a>Tabella Sysssispackages  
 La tabella **sysssispackages** in `msdb` contiene i pacchetti salvati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql).  
  
 Le colonne della tabella **sysssispackages** contengono informazioni sui ruoli assegnati ai pacchetti.  
  
-   Nella colonna **readerrole** è indicato il ruolo con accesso in lettura al pacchetto.  
  
-   Nella colonna **writerrole** è indicato il ruolo con accesso in scrittura al pacchetto.  
  
-   La colonna **ownersid** include l'ID di sicurezza (SID) univoco dell'utente che ha creato il pacchetto. Questa colonna definisce pertanto il proprietario del pacchetto.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, le autorizzazioni del `db_ssisadmin` e **db_ssisoperator** i ruoli predefiniti a livello di database e l'ID di sicurezza univoco dell'utente che ha creato il pacchetto si applicano al ruolo lettore per i pacchetti, mentre le autorizzazioni del `db_ssisadmin` ruolo e l'ID di sicurezza univoco dell'utente che ha creato il pacchetto si applicano al ruolo writer. `db_ssisadmin`Per disporre dell'accesso in lettura al pacchetto, un utente deve essere un membro del ruolo, **db_ssisltduser**o **db_ssisoperator** . Un utente deve essere membro del `db_ssisadmin` ruolo per avere accesso in scrittura.  
  
## <a name="access-to-packages"></a>Accesso ai pacchetti  
 I ruoli predefiniti del database funzionano congiuntamente ai ruoli definiti dall'utente, ovvero i ruoli creati dall'utente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e usati per l'assegnazione di autorizzazioni ai pacchetti. Per poter accedere a un pacchetto, un utente deve essere membro del ruolo definito dall'utente e del ruolo predefinito del database di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] appropriato. Se, ad esempio, gli utenti sono membri del ruolo definito dall'utente **AuditUsers** assegnato a un pacchetto, devono essere anche membri del `db_ssisadmin` ruolo, **db_ssisltduser**o **db_ssisoperator** per disporre dell'accesso in lettura al pacchetto.  
  
 Se non si assegna alcun ruolo definito dall'utente ai pacchetti, l'accesso verrà determinato dai ruoli predefiniti a livello di database.  
  
 Se si desidera utilizzare ruoli definiti dall'utente, è necessario aggiungerli al `msdb` database prima di poterli assegnare ai pacchetti. È possibile creare nuovi ruoli del database in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 I ruoli a livello di database di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] concedono diritti per le tabelle di sistema di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel database msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]per potersi connettere al motore di database e accedere al database, è necessario avviare il servizio MSSQLSERVER `msdb` .  
  
 Per assegnare ruoli ai pacchetti, è necessario completare le attività seguenti.  
  
-   **Aprire Esplora oggetti e connettersi a Integration Services**  
  
     Per poter assegnare ruoli ai pacchetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è necessario aprire Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e connettersi a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Per poter eseguire la connessione a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è necessario che il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sia stato avviato.  
  
-   **Assegnazione dei ruoli lettura e scrittura ai pacchetti**  
  
     È possibile assegnare un ruolo lettura o scrittura a ogni pacchetto.  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Assegnazione di un ruolo lettura e scrittura a un pacchetto](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Creazione di un ruolo definito dall'utente](../create-a-user-defined-role.md)  
  
-   [Connessione a Integration Services](../connect-to-integration-services.md)  
  
  
