---
title: Configurare un server di destinazione| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a001509cba1ef02182963fd8d8f8946f95321ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659839"
---
# <a name="make-a-target-server"></a>Configurare un server di destinazione
  In questo argomento viene descritto come configurare un server di destinazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o SQL Server Management Objects (SMO).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per configurare un server di destinazione utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
 I processi distribuiti con passaggi associati a un proxy vengono eseguiti nel contesto dell'account proxy nel server di destinazione. Verificare che siano soddisfatte le condizioni seguenti, per assicurare che i passaggi di processo associati a un proxy vengano scaricati dal server master a quello di destinazione:  
  
-   La sottochiave del Registro di sistema di server master **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<*nome_istanza*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName**  (REG_DWORD) è impostato su 1 (true). Per impostazione predefinita, questa sottochiave è impostata su 0 (False).  
  
-   Nel server di destinazione deve esistere un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio del processo.  
  
 Se si verificano errori nel download dei passaggi dei processi che usano account proxy dal server master a quello di destinazione, è possibile controllare se nella colonna **error_message** della tabella **sysdownloadlist** nel database **msdb** sono presenti i messaggi di errore seguenti:  
  
-   "Per questo passaggio del processo è necessario un account proxy, ma l'individuazione dei proxy è disabilitata nel server di destinazione."  
  
     Per risolvere il problema, impostare la sottochiave del Registro di sistema **AllowDownloadedJobsToMatchProxyName** su 1.  
  
-   "Impossibile trovare il proxy."  
  
     Per risolvere il problema, verificare che nel server di destinazione sia disponibile un account proxy con lo stesso nome dell'account proxy del server master utilizzato per l'esecuzione del passaggio di processo.  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per questa procedura vengono assegnate per impostazione predefinita ai membri del ruolo predefinito del server `sysadmin`.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>Per configurare un server di destinazione  
  
1.  In **Esplora oggetti** connettersi a un'istanza del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espanderla.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Imposta come server di destinazione**. **Configurazione guidata server di destinazione** consente di eseguire in modo semplificato i passaggi necessari per configurare un server di destinazione.  
  
3.  Nella pagina **Selezione server master** selezionare il server master dal quale il server di destinazione corrente riceverà i processi.  
  
     **Seleziona server**  
     Tramite questa opzione è possibile connettersi al server master.  
  
     **Descrizione del server**  
     Consente di digitare una descrizione del server di destinazione corrente. Tale descrizione verrà caricata sul server master dal server di destinazione.  
  
4.  Nella pagina **Credenziali account di accesso al server master** creare un nuovo account di accesso al server di destinazione, se necessario.  
  
     **Crea un nuovo account di accesso se necessario e assegna i diritti per il server MSX**  
     Tramite questa opzione è possibile creare un nuovo account di accesso nel server di destinazione se l'account di accesso specificato non esiste già.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>Per configurare un server di destinazione  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio il server corrente viene integrato nel server master AdventureWorks1. L'ubicazione del server corrente è Building 21, Room 309, Rack 5.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     Per altre informazioni, vedere [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
##  <a name="PowerShellProcedure"></a> Usando SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione automatizzata in un'organizzazione](automated-administration-across-an-enterprise.md)  
  
  
