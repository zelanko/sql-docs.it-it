---
title: Reimpostazione della password
description: La pagina di reimpostazione della password consente di modificare la password per gli account amministratore usati da Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400899"
---
# <a name="password-reset---analytics-platform-system"></a>Reimpostazione password-sistema della piattaforma di analisi
La pagina di **reimpostazione della password** consente di modificare la password per gli account amministratore usati da Analytics Platform System.  
  
> [!WARNING]  
> Usare sempre il **Configuration Manager** per aggiornare la password dell'amministratore di dominio del dispositivo. Altri metodi potrebbero non aggiornare tutti i componenti del sistema di piattaforma di analisi e potrebbero causare problemi di accesso alle appliance.  
  
Quando il dispositivo viene recapitato, vengono fornite le password di sistema della piattaforma di analisi. Modificare sempre le password in nuovi valori quando si assume la responsabilità dell'appliance. Sono disponibili tre password da aggiornare. Le password non devono necessariamente essere le stesse.  
  
**F<*xxxx*> \Administrator**  
**Amministratore** del dominio dell'appliance.  
  
**.\Administrator**  
L'account **amministratore** locale nei computer che ospitano le macchine virtuali.  
  
> [!IMPORTANT]  
> Per l'aggiornamento del dispositivo 1, **Configuration Manager** non modifica correttamente la password degli account amministratore locale in tutte le VM PDW. Se necessario, contattare il servizio supporto tecnico clienti per istruzioni aggiuntive.  
  
**SA**  
Account di accesso **sa** in SQL Server. **sa** è un membro del ruolo predefinito del server **sysadmin** ed è un amministratore SQL Server. Per modificare la password dell'account di accesso **sa** , è inoltre possibile utilizzare l'istruzione **ALTER LOGIN** .  
  
## <a name="password-requirements"></a>Requisiti per le password  
Sia le credenziali di amministratore di dominio sia le credenziali di amministratore di sistema rispettano i criteri di complessità delle password per ogni tipo di credenziale. Quando si modificano le credenziali di amministratore di dominio, la nuova password viene aggiornata nel dominio in cui è necessario in SQL Server PDW.  
  
> [!IMPORTANT]  
> SQL Server PDW non supporta il segno di dollaro (**$**) nelle password di amministratore di dominio o di amministratore locale. I caratteri **^% &** sono consentiti nelle password, tuttavia PowerShell li considera come caratteri speciali. Se uno di questi caratteri viene usato nelle password per l'amministratore di sistema o SQL Server account**sa** (i parametri **AdminPassword** e **PdwSAPassword** durante l'installazione), il programma di installazione, tra cui install, Upgrade, REPLACENODE e patching, avrà esito negativo. Per garantire un aggiornamento corretto quando le password correnti contengono caratteri non supportati, modificare le password in modo che non contengano tali caratteri prima di eseguire l'aggiornamento. Al termine dell'aggiornamento, è possibile impostare di nuovo le password sui valori originali. Per ulteriori informazioni sui requisiti relativi alle password, vedere [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Per reimpostare la password  
  
1.  Connettersi al nodo di controllo e avviare il **Configuration Manager** (**dwconfig. exe**). Per ulteriori informazioni, vedere [la pagina relativa all'avvio del&#41;di sistema della piattaforma Configuration Manager &#40;Analytics ](launch-the-configuration-manager.md).  
  
2.  Nel riquadro sinistro della **Configuration Manager**fare clic su **reimpostazione password**.  
  
3.  Selezionare il tipo di amministratore dal menu a discesa **account** , quindi immettere la nuova password nelle caselle **password** e **Conferma password** . Fare clic su **applica** per salvare le modifiche.  
  
    Le modifiche apportate a questi account non influiscono sulle sessioni attualmente attive, ma verranno applicate al successivo tentativo di accesso per ogni utente.  
  
    ![SQL Server - Password DWConfig](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Vedere anche  
[Impostare la password amministratore per l'accesso ai nodi AD in modalità ripristino servizi directory &#40;il sistema della piattaforma di&#41; &#40;Analytics&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Avviare la piattaforma Configuration Manager &#40;Analytics System&#41;](launch-the-configuration-manager.md)  
  
