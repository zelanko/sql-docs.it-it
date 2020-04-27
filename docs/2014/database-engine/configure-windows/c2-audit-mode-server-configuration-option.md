---
title: Opzione di configurazione del server c2 audit mode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0233f6c40e15fd4f612002854477d98068901b15
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786670"
---
# <a name="c2-audit-mode-server-configuration-option"></a>Opzione di configurazione del server c2 audit mode
  È possibile configurare l'opzione C2 audit mode tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o con l'opzione **c2 audit mode** in **sp_configure**. Questa opzione consente di configurare il server per la registrazione dei tentativi di accesso alle istruzioni e agli oggetti riusciti e non riusciti. Tali informazioni risultano utili per documentare l'attività del server e per tenere traccia delle possibili violazioni dei criteri di sicurezza  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Lo standard di sicurezza C2 è stato sostituito dalla certificazione con criteri comuni. Vedere [Opzione di configurazione del server common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md).  
  
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
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
