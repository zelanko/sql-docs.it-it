---
title: Connettersi a SQL Server se gli amministratori di sistema sono bloccati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 6d493629c8b0564467155c3eae6ac05e25c5105c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767967"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>Connettersi a SQL Server se gli amministratori di sistema sono bloccati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come ottenere nuovamente l'accesso al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] come amministratore di sistema. Un amministratore di sistema può perdere l'accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per uno dei motivi seguenti:  
  
-   Tutti gli account di accesso membri del ruolo predefinito del server sysadmin sono stati rimossi per errore.  
  
-   Tutti i gruppi di Windows membri del ruolo predefinito del server sysadmin sono stati rimossi per errore.  
  
-   Gli account di accesso membri del ruolo predefinito del server sysadmin sono assegnati a utenti che hanno lasciato la società o che non sono disponibili.  
  
-   L'account sa è disabilitato o la password non è nota ad alcun utente.  
  
 Un metodo per ottenere nuovamente l'accesso consiste nel reinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nel collegare tutti i database alla nuova istanza. Questa soluzione richiede molto tempo. Per recuperare gli account di accesso, inoltre, può essere necessario ripristinare il database master da un backup. Se il backup del database master è meno recente, potrebbe non contenere tutte le informazioni. Se il backup del database master è più recente, potrebbe includere gli stessi account di accesso dell'istanza precedente e, pertanto, gli amministratori possono risultare ancora bloccati.  
  
## <a name="resolution"></a>Soluzione  
 Avviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo usando l'opzione **-m** o **-f** . Qualsiasi membro del gruppo Administrators locale del computer potrà quindi connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come membro del ruolo predefinito del server sysadmin.  
  
> [!NOTE]  
>  Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, arrestare innanzitutto il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe eseguire per primo la connessione impedendo la connessione come secondo utente.  
  
 Quando si usa l'opzione **-m** con **sqlcmd** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile limitare le connessioni a un'applicazione client specifica. Ad esempio, **-m"sqlcmd"** limita le connessioni a una singola connessione, che deve identificarsi come programma client **sqlcmd** . Utilizzare questa opzione quando si avvia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo e un'applicazione client sconosciuta accede all'unica connessione disponibile. Per connettersi con l'editor di query in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], usare **-m"Microsoft SQL Server Management Studio - Query"** .  
  
> [!IMPORTANT]  
>  Non utilizzare tale opzione come caratteristica di sicurezza. L'applicazione client fornisce il nome dell'applicazione client stessa e può indicare un nome falso come parte della stringa di connessione.  
  
 Per istruzioni dettagliate su come avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità utente singolo, vedere [Configurare le opzioni di avvio Server &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="step-by-step-instructions"></a>Istruzioni dettagliate  
 Nelle istruzioni seguenti viene illustrato il processo per la connessione a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in esecuzione in Windows 8 o versione successiva. Sono fornite delle lievi modifiche per le versioni precedenti di SQL Server o Windows. Queste istruzioni devono essere eseguite quando si effettua l'accesso a Windows come membro del gruppo di amministratori locali e si presuppone che nel computer sia installato [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
1.  Nella pagina iniziale avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Selezionare **Server registrati** dal menu **Visualizza**. Se il server non è ancora registrato, fare clic con il pulsante destro del mouse su **Gruppi di server locali**, scegliere **Attività**e quindi **Registra server locali**.  
  
2.  Nell'area Server registrati fare clic con il pulsante destro del mouse sul server e quindi scegliere **Gestione configurazione SQL Server**. Dovrebbe essere visualizzata la richiesta di autorizzazione all'esecuzione come amministratore. Successivamente, aprire il programma Gestione configurazione.  
  
3.  Chiudere [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Nel riquadro a sinistra di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare **Servizi di SQL Server**. Nel riquadro a destra individuare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nell'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è incluso **(MSSQLSERVER)** dopo il nome del computer. Le istanze denominate vengono visualizzate in maiuscolo con lo stesso nome presente in Server registrati. Fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi scegliere **Proprietà**.  
  
5.  Nella casella **Specificare un parametro di avvio** della scheda **Parametri di avvio** digitare `-m` (ovvero un trattino seguito dalla lettera m minuscola) e quindi fare clic su **Aggiungi**. .  
  
    > [!NOTE]  
    >  In alcune versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è presente alcuna scheda **Parametri di avvio** . In questo caso, nella scheda **Avanzate** fare doppio clic su **Parametri di avvio**. I parametri vengono visualizzati in una finestra molto piccola. Fare attenzione a non modificare nessuno dei parametri esistenti. Al termine, aggiungere un nuovo parametro `;-m` (ovvero un punto e virgola seguito da un trattino e una lettera m minuscola) e quindi fare clic su **OK**. .  
  
6.  Fare clic su **OK**e, dopo il messaggio di riavvio, fare clic con il pulsante destro del mouse sul nome del server e quindi scegliere **Riavvia**.  
  
7.  Dopo il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il server sarà in modalità utente singolo. Accertarsi che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non sia in esecuzione, altrimenti l'unica connessione presente non sarà più disponibile a causa del relativo utilizzo da parte di questo servizio.  
  
8.  Nella schermata iniziale di Windows 8 fare clic con il pulsante destro del mouse sull'icona di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Nella parte inferiore della schermata selezionare **Esegui come amministratore**. (le credenziali di amministratore verranno passate in SSMS).  
  
    > [!NOTE]  
    >  Per le versioni precedenti di Windows, l'opzione **Esegui come amministratore** viene visualizzata come sottomenu.  
  
     In alcune configurazioni, tramite SSMS si tenterà di stabilire diverse connessioni. Non sarà possibile stabilire più connessioni poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in modalità utente singolo. È possibile scegliere di effettuare una delle azioni riportate di seguito.  
  
    1.  Effettuare la connessione con Esplora oggetti mediante l'autenticazione di Windows (in cui sono incluse le credenziali di amministratore). Espandere **Sicurezza**, **Account di accesso**e fare doppio clic sul proprio account di accesso. Nella pagina **Ruoli server** selezionare **sysadmin**quindi fare clic su **OK**.  
  
    2.  Anziché effettuare la connessione con Esplora oggetti, utilizzare una finestra Query tramite l'autenticazione di Windows (in cui sono incluse le credenziali di amministratore) (si tratta dell'unica modalità di connessione possibile se non è stato utilizzato Esplora oggetti). Eseguire codice come il seguente per aggiungere un nuovo account di accesso con autenticazione di Windows che fa parte del ruolo predefinito del server **sysadmin**. Nell'esempio seguente viene aggiunto un utente di dominio denominato `CONTOSO\PatK`.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione nella modalità di autenticazione mista, effettuare la connessione con una finestra Query utilizzando l'autenticazione di Windows (in cui sono incluse le credenziali di amministratore). Eseguire codice come il seguente per creare un nuovo account di accesso con autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che fa parte del ruolo predefinito del server **sysadmin** .  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  Sostituire ************ con una password complessa.  
  
    4.  Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione nella modalità di autenticazione mista e si vuole reimpostare la password dell'account **sa** , eseguire la connessione con una finestra Query usando l'autenticazione di Windows, che include le credenziali di amministratore. Modificare la password dell'account **sa** con la sintassi seguente.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  Sostituire ************ con una password complessa.  
  
9. Tramite i passaggi seguenti viene ora di nuovo impostata la modalità multiutente per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Chiudere SSMS.  
  
10. Nel riquadro a sinistra di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare **Servizi di SQL Server**. Nel riquadro a destra fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e quindi scegliere **Proprietà**.  
  
11. Nella casella **Parametri esistenti** della scheda **Parametri di avvio** selezionare `-m` e quindi fare clic su **Rimuovi**.  
  
    > [!NOTE]  
    >  In alcune versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è presente alcuna scheda **Parametri di avvio** . In questo caso, nella scheda **Avanzate** fare doppio clic su **Parametri di avvio**. I parametri vengono visualizzati in una finestra molto piccola. Rimuovere i caratteri `;-m` aggiunti in precedenza e fare clic su **OK**.  
  
12. Fare clic con il pulsante destro del mouse sul nome del server e quindi scegliere **Riavvia**.  
  
 A questo punto è possibile connettersi normalmente con uno degli account che fa parte del ruolo predefinito del server **sysadmin** .  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio di SQL Server in modalità utente singolo](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [Opzioni di avvio del servizio del motore di database](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
