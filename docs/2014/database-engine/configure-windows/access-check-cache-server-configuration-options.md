---
title: Opzioni di configurazione del server access check cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a82aa2872f5a1e1658ab3d736c2651253bb7cc74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812044"
---
# <a name="access-check-cache-server-configuration-options"></a>Opzioni di configurazione del server access check cache
  Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]accede agli oggetti di database, il controllo dell'accesso viene memorizzato nella cache in una struttura interna denominata **cache dei risultati del controllo dell'accesso**. Le opzioni **access check cache quota** e **access check cache bucket count** determinano il numero di voci e di hash bucket utilizzati per **la cache dei risultati del controllo dell'accesso**. Raramente la modifica di tali opzioni consente di ottenere prestazioni migliori.  
  
 Il valore predefinito 0 indica che le opzioni vengono gestite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . È consigliabile modificare le opzioni solo se suggerito dal Servizio Supporto Tecnico Clienti Microsoft.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
