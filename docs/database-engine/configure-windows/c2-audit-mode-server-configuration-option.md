---
title: Opzione di configurazione del server c2 audit mode | Microsoft Docs
description: Acquisire familiarità con c2 audit mode, un'opzione di configurazione di SQL Server che consente di profilare l'attività del sistema e tenere traccia delle possibili violazioni dei criteri di sicurezza.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], C2 Audit Mode option
- C2 auditing
- C2 Audit Mode option
- recording attempts
ms.assetid: 5a8d73a6-c4f6-4967-ba11-ecbcfc90b9cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d92dcad571574310c1b64a9992a54b166fe8ad8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759202"
---
# <a name="c2-audit-mode-server-configuration-option"></a>Opzione di configurazione del server c2 audit mode
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  È possibile configurare l'opzione C2 audit mode tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o con l'opzione **c2 audit mode** in **sp_configure**. Questa opzione consente di configurare il server per la registrazione dei tentativi di accesso alle istruzioni e agli oggetti riusciti e non riusciti. Tali informazioni risultano utili per documentare l'attività del server e per tenere traccia delle possibili violazioni dei criteri di sicurezza  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Lo standard di sicurezza C2 è stato sostituito dalla certificazione con criteri comuni. Vedere [Opzione di configurazione del server common criteria compliance enabled](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
  
## <a name="audit-log-file"></a>File di log di controllo  
 I dati impostati tramite l'opzione C2 audit mode vengono salvati in un file nella directory predefinita dei dati dell'istanza. Se la dimensione del file raggiunge il limite di 200 megabyte (MB), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un nuovo file, chiude il vecchio file e scrive tutti i nuovi record di controllo nel nuovo file. Il processo continua fino al riempimento della directory dei dati di controllo o alla disabilitazione della funzione di controllo. Per determinare lo stato di una traccia C2, eseguire una query sulla vista del catalogo sys.traces.  
  
> [!IMPORTANT]  
>  L'opzione c2 audit mode consente di salvare una grande quantità di informazioni nel file di log, che può raggiungere rapidamente dimensioni notevoli. Se non è più disponibile spazio nella directory in cui vengono salvati i log, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si chiuderà automaticamente. Se per la funzione di controllo è impostato l'avvio automatico, è necessario riavviare l'istanza con il flag **-f** (che ignora la funzione di controllo) oppure liberare spazio su disco per il log di controllo.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene abilitata l'opzione C2 audit mode.  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
sp_configure 'c2 audit mode', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
