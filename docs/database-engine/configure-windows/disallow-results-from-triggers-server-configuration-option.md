---
title: Opzione di configurazione del server disallow results from triggers | Microsoft Docs
description: Informazioni sull'opzione 'disallow results from triggers'. Scoprire come può impedire problemi nelle applicazioni che non sono progettate per interagire con i set di risultati.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8cbe799b72a88da9785e778cb0688fe3ff1a3f44
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772523"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>Impostazione di configurazione del server disallow results from triggers
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'opzione **Disallow Results From Triggers** consente di specificare se i trigger debbano o meno restituire set di risultati. I trigger che restituiscono set di risultati possono provocare comportamenti imprevisti nelle applicazioni che non sono state progettate per il loro utilizzo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] È consigliabile impostare questo valore su 1.  
  
 Se il valore è 1, l'opzione **Disallow Results From Triggers** è impostata su ON. L'impostazione predefinita per questa opzione è 0 (OFF). Se l'opzione è impostata su 1 (ON), qualsiasi tentativo da parte di un trigger di restituire un set di risultati ha esito negativo e l'utente riceve il messaggio di errore seguente:  
  
 "Msg 524, Livello 16, Stato 1, Procedura \<Procedure Name>, Riga \<Line#>  
  
 "Un trigger ha restituito un set di risultati e l'opzione del server 'disallow_results_from_triggers' è impostata su true".  
  
 L'opzione **disallow results from triggers** viene applicata a livello di istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e determina il comportamento di tutti i trigger esistenti nell'istanza.  
  
 **Disallow Results From Triggers** è un'opzione avanzata. Se per modificare l'impostazione si usa la stored procedure di sistema **sp_configure** , sarà possibile modificare Disallow Results From Triggers solo quando il valore di **Show Advanced Options** è impostato su 1. L'impostazione diventa effettiva immediatamente e non richiede il riavvio del server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
