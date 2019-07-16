---
title: Reimpostazione della password - sistema di piattaforma Analitica | Microsoft Docs
description: La pagina di reimpostazione della Password consente di modificare la password per gli account amministratore usato dal sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5fb3bbb5adba5754c220c34503a22656f6da39c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960464"
---
# <a name="password-reset---analytics-platform-system"></a>Reimpostazione della password - sistema di piattaforma Analitica
Il **reimpostazione delle Password** pagina consente di modificare la password per gli account amministratore usato dal sistema di piattaforma Analitica.  
  
> [!WARNING]  
> Usare sempre la **Configuration Manager** per aggiornare la password di amministratore di dominio appliance. Altri metodi di non essere aggiornati tutti i componenti di sistema di piattaforma Analitica e potrebbe causare problemi di accesso dell'appliance.  
  
Viene fornita la password del sistema di piattaforma Analitica quando viene recapitata all'appliance. Sempre modificare le password per i nuovi valori quando si assumersi la responsabilità per l'appliance. Vi sono tre le password per l'aggiornamento. Le password non sono necessario essere quella di loro.  
  
**F <*xxxx*> \administrator.**  
Il **amministratore** del dominio appliance.  
  
**.\Administrator**  
Locale **amministratore** account nei computer che ospitano le macchine virtuali.  
  
> [!IMPORTANT]  
> Aggiornamento 1, per appliance **Configuration Manager** non correttamente non modifica la password dell'account di amministratore locale in tutto il PDW VM. Se è necessario, contattare il Microsoft per ulteriori istruzioni.  
  
**sa**  
Il **sa** account di accesso in SQL Server. **SA** è un membro del **sysadmin** ruolo predefinito del server e sia un amministratore di SQL Server. La password del **sa** account di accesso può essere modificato anche tramite il **ALTER LOGIN** istruzione.  
  
## <a name="password-requirements"></a>Requisiti delle password  
Sia le credenziali di amministratore di dominio e le credenziali di amministratore di sistema rispettano i criteri di complessità delle password per ogni tipo di credenziale. Quando si modificano le credenziali di amministratore di dominio, la nuova password viene aggiornata per il dominio in cui è necessaria in SQL Server PDW.  
  
> [!IMPORTANT]  
> SQL Server PDW non supporta il carattere di segno di dollaro ( **$** ) nell'amministratore di dominio o le password di amministratore locale. I caratteri **^ % &** sono consentiti nelle password, ma PowerShell considera come caratteri speciali. Se uno di questi caratteri vengono usato per le password per l'amministratore di sistema o SQL Server**sa** account (il **AdminPassword** e **PdwSAPassword** parametri durante programma di installazione) per l'installazione, tra cui INSTALL, UPGRADE, REPLACENODE e l'applicazione di patch, avrà esito negativo. Per garantire una corretta esecuzione dell'aggiornamento quando le password corrente contengono caratteri non supportati, modificare le password in modo che non contengono tali caratteri prima di eseguire l'aggiornamento. Al termine dell'aggiornamento, è possibile impostare le password nuovamente i valori originali. Per altre informazioni sui requisiti della password, vedere [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Per reimpostare una password  
  
1.  Connettersi al nodo di controllo e avviare il **Configuration Manager** (**dwconfig.exe**). Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della finestra di **Configuration Manager**, fare clic su **reimpostazione della Password**.  
  
3.  Selezionare il tipo di amministratore dal **Account** dal menu a discesa e quindi immettere la nuova password nel **Password** e **Conferma Password** caselle. Fare clic su **applica** per salvare le modifiche.  
  
    Le modifiche apportate a tali account non influiscono le sessioni attualmente attive, ma verranno applicate al successivo tentativo di accesso per ogni utente.  
  
    ![SQL Server DWConfig Password](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Vedere anche  
[Impostare la Password di amministratore per l'accesso ai nodi AD in modalità ripristino servizi Directory &#40;modalità ripristino servizi directory&#41; &#40;sistema di piattaforma Analitica&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)  
  
