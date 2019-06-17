---
title: Configurazione motore - istanza utente di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ba05d426f9515793ad3a924e375ff9a6ab9f940f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095875"
---
# <a name="database-engine-configuration---user-instance"></a>Configurazione del Motore di database – Istanze utente
  Utilizzare la pagina **Istanze utente** per generare un'istanza distinta del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per gli utenti che non dispongono di autorizzazioni di amministratore, nonché per aggiungere utenti al ruolo di amministratore.  
  
## <a name="option"></a>Opzione  
 Attiva istanze utente  
 Per impostazione predefinita questa opzione è abilitata. Per disabilitare la funzionalità di attivazione delle istanze utente, deselezionare la casella di controllo.  
  
 L'istanza utente, nota anche come istanza figlio o client, è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generata dall'istanza padre (l'istanza primaria eseguita come servizio, ad esempio [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) per conto di un utente. L'istanza utente viene eseguita come processo utente nel contesto di sicurezza di tale utente. L'istanza utente è isolata dall'istanza padre e da qualsiasi altra istanza che viene eseguita nel computer. Questa caratteristica è nota anche come RANU (Run As Normal User).  
  
> [!NOTE]  
>  Per gli account di accesso di cui è stato eseguito il provisioning come membri del ruolo predefinito del server **sysadmin** in fase di configurazione, viene effettuato il provisioning come amministratori nel database dei modelli. Gli account rimarranno membri del ruolo predefinito del server **sysadmin** nell'istanza utente, a meno che non vengano rimossi  
  
 Aggiungi utente al ruolo di amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Per impostazione predefinita, questa opzione non è abilitata. Per aggiungere l'utente dell'installazione corrente al ruolo di amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare la casella di controllo.  
  
 Gli utenti di [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] che sono membri di BUILTIN\Administrators non vengono automaticamente aggiunti al ruolo predefinito del server sysadmin quando si connettono a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Solo gli utenti di [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] aggiunti esplicitamente a un ruolo di amministratore a livello di server possono amministrare [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Tutti i membri del gruppo Built-In\Users possono connettersi all'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , ma dispongono di autorizzazioni limitate per l'esecuzione delle operazioni relative al database. Agli utenti che ereditano i privilegi di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] dai gruppi BUILTIN\Administrators e Built-In\Users delle versioni precedenti di Windows devono pertanto essere concessi esplicitamente privilegi amministrativi nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in esecuzione in [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Per apportare modifiche ai ruoli utente al termine del programma di installazione, utilizzare lo strumento Configurazione superficie di attacco (SQLSAC.exe) di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Per aggiornare l'elenco degli utenti nel ruolo di amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic sul collegamento **Aggiungi nuovo amministratore** .  
  
 Verificare che il campo **Utente a cui concedere i privilegi** contenga DomainName\UserName dell'utente le cui autorizzazioni devono essere aggiornate. Nell'elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluso nel riquadro **Privilegi disponibili** selezionare il ruolo da aggiornare e quindi fare clic sulla freccia a destra. Per aggiungere l'utente a tutti i ruoli disponibili per tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic sulla doppia freccia a destra.  
  
 Al termine delle selezioni, [!INCLUDE[clickOK](../../includes/clickok-md.md)]per implementare le modifiche apportate. Per chiudere lo strumento senza apportare alcuna modifica, fare clic su **Annulla**.  
  
  
