---
title: Scrittura di eventi di controllo di SQL Server nel registro di sicurezza | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 53f613bd2a791eb210d908e3e84f8f09098db977
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62715878"
---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>Scrittura di eventi di controllo di SQL Server nel registro di sicurezza  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In un ambiente con sicurezza elevata il registro di sicurezza di Windows rappresenta la posizione appropriata per la scrittura di eventi che registrano l'accesso agli oggetti. Sono supportati altre posizioni di controllo che tuttavia sono più soggette alla manomissione.  
  
 La scrittura dei controlli del server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel registro di sicurezza di Windows prevede due requisiti fondamentali:  
  
-   È necessario configurare l'impostazione di controllo dell'accesso agli oggetti per l'acquisizione degli eventi. Lo strumento dei criteri di controllo (`auditpol.exe`) espone varie impostazioni di criteri secondari nella categoria **controllo dell'accesso agli oggetti** . Per consentire il controllo dell'accesso agli oggetti in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , configurare l'impostazione **generata dall'applicazione** .  
-   L'account in cui viene eseguito il servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre dell'autorizzazione **generazione controlli di sicurezza** per scrivere nel registro di sicurezza di Windows. Per impostazione predefinita, gli account LOCAL SERVICE e NETWORK SERVICE dispongono di questa autorizzazione. Questo passaggio non è obbligatorio se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito in uno di questi account.  
-   Concedere l'autorizzazione completa per l'account del servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]all'hive del Registro di sistema `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Security`.  

  > [!IMPORTANT]  
  > [!INCLUDE[ssnoteregistry-md](../../../includes/ssnoteregistry-md.md)]   
  
I criteri di controllo di Windows possono influire sul controllo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se sono configurati per scrivere nel registro di sicurezza di Windows. Se i criteri di controllo non sono configurati in modo corretto, potrebbe verificarsi la perdita di eventi. In genere il registro di sicurezza di Windows è impostato in modo che gli eventi meno recenti vengano sovrascritti e vengano mantenuti quelli più recenti. Tuttavia, se il registro di sicurezza di Windows è impostato in modo diverso e il registro di sicurezza è pieno, verrà generato l'evento di Windows 1104 che indica che il registro è pieno. A questo punto si verificano le situazioni seguenti:  
-   Non verranno registrati ulteriori eventi di sicurezza  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non potrà rilevare che il sistema non è in grado di registrare gli eventi nel registro di sicurezza, causando una perdita potenziale di eventi di controllo  
-   Dopo che l'amministratore ha apportato correzioni al registro di sicurezza, il comportamento relativo alla registrazione tornerà normale.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 Gli amministratori del computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono comprendere che le impostazioni locali relative al registro di sicurezza possono essere sovrascritte da criteri del dominio. In questo caso i criteri del dominio potrebbero sovrascrivere l'impostazione della sottocategoria (**auditpol/get/subcategory:"application generated"** ). Questa condizione può influire sulla possibilità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di registrare eventi senza disporre di alcuna modalità per rilevare che gli eventi che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sta tentando di controllare non verranno registrati.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario essere amministratore di Windows per configurare queste impostazioni.  
  
##  <a name="auditpolAccess"></a> Per configurare l'impostazione di controllo dell'accesso agli oggetti in Windows mediante auditpol  
  
1.  Aprire un prompt dei comandi con autorizzazioni amministrative.  
  
    1.  Nel menu **Start** scegliere **Tutti i programmi**, **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi fare clic su **Esegui come amministratore**.  
  
    2.  Se viene visualizzata la finestra di dialogo **Controllo account utente** , fare clic su **Continua**.  
  
2.  Eseguire l'istruzione seguente per abilitare il controllo da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  Chiudere la finestra del prompt dei comandi.  
  
##  <a name="secpolAccess"></a> Per concedere l'autorizzazione di generazione dei controlli di sicurezza a un account mediante secpol  
  
1.  Per qualsiasi sistema operativo Windows, scegliere **Esegui** dal menu **Start**.  
  
2.  Digitare **secpol.msc** , quindi fare clic su **OK**. Se viene visualizzata la finestra di dialogo **Controllo account utente** , fare clic su **Continua**.  
  
3.  Nello strumento Criteri di sicurezza locale espandere **Impostazioni di sicurezza**, **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
4.  Nel riquadro dei risultati fare doppio clic su **Generazione di controlli di sicurezza**.  
  
5.  Nella scheda **Impostazioni di sicurezza locali** fare clic su **Aggiungi utente o gruppo**.  
  
6.  Nella finestra di dialogo **Seleziona utenti, computer o gruppi** digitare il nome dell'account utente, ad esempio **dominio1\utente1** , quindi fare clic su **OK**oppure su **Avanzate** e cercare l'account.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  Chiudere lo strumento Criteri di sicurezza.  
  
9. Riavviare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per abilitare questa impostazione.  
  
##  <a name="secpolPermission"></a> Per configurare l'impostazione di controllo dell'accesso agli oggetti in Windows mediante secpol  
  
1.  Se si utilizza un sistema operativo precedente a [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] o Windows Server 2008, scegliere **Esegui** dal menu **Start**.  
  
2.  Digitare **secpol.msc** , quindi fare clic su **OK**. Se viene visualizzata la finestra di dialogo **Controllo account utente** , fare clic su **Continua**.  
  
3.  Nello strumento Criteri di sicurezza locale espandere **Impostazioni di sicurezza**, **Criteri locali**, quindi fare clic su **Criteri di controllo**.  
  
4.  Nel riquadro dei risultati fare doppio clic su **Controlla accesso agli oggetti**.  
  
5.  Nella scheda **Impostazioni di sicurezza locali** , nell'area **Controlla i seguenti tentativi** selezionare sia **Esito positivo** sia **Esito negativo**.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Chiudere lo strumento Criteri di sicurezza.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Audit &#40;Motore di database&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
