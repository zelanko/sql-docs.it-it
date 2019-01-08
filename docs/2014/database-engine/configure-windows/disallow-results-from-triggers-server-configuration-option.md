---
title: Opzione di configurazione del server disallow results from triggers | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0606379484fe14b0dfa1d93b604b8ee2b6eb7981
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641222"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>Impostazione di configurazione del server disallow results from triggers
  L'opzione **Disallow Results From Triggers** consente di specificare se i trigger debbano o meno restituire set di risultati. I trigger che restituiscono set di risultati possono provocare comportamenti imprevisti nelle applicazioni che non sono state progettate per il loro utilizzo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] È consigliabile impostare questo valore su 1.  
  
 Se il valore è 1, l'opzione **Disallow Results From Triggers** è impostata su ON. L'impostazione predefinita per questa opzione è 0 (OFF). Se l'opzione è impostata su 1 (ON), qualsiasi tentativo da parte di un trigger di restituire un set di risultati ha esito negativo e l'utente riceve il messaggio di errore seguente:  
  
 "Msg 524, livello 16, stato 1, procedura \<nome procedura>, riga \<numero riga>  
  
 "Un trigger ha restituito un set di risultati e l'opzione del server 'disallow_results_from_triggers' è impostata su true".  
  
 L'opzione **Disallow Results From Triggers** viene applicata a livello di istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e determina il comportamento di tutti i trigger esistenti nell'istanza.  
  
 **Disallow Results From Triggers** è un'opzione avanzata. Se per modificare l'impostazione si usa la stored procedure di sistema **sp_configure** , sarà possibile modificare Disallow Results From Triggers solo quando il valore di **Show Advanced Options** è impostato su 1. L'impostazione diventa effettiva immediatamente e non richiede il riavvio del server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
