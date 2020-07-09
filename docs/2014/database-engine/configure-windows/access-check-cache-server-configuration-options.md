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
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158759"
---
# <a name="access-check-cache-server-configuration-options"></a>Opzioni di configurazione del server access check cache
Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]accede agli oggetti di database, il controllo dell'accesso viene memorizzato nella cache in una struttura interna denominata **cache dei risultati del controllo dell'accesso**. 
  
L'opzione **Access check cache bucket count** controlla il numero di bucket di hash utilizzati per la cache dei risultati del controllo dell'accesso. 

L'opzione **Access check cache quota** controlla il numero di voci archiviate nella cache dei risultati del controllo dell'accesso. Quando viene raggiunto il numero massimo di voci, le voci meno recenti vengono rimosse dalla cache dei risultati del controllo dell'accesso.
  
Il valore predefinito 0 indica che le opzioni vengono gestite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Da [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a, i valori predefiniti vengono convertiti nelle configurazioni interne seguenti:
-   Per Access check cache bucket count, il valore 0 imposta un valore predefinito di 256 bucket per l'architettura x86 e 2.048 bucket per le architetture x64 e IA-64.
-   Per Access check cache quota, il valore 0 imposta un valore predefinito di 1.024 voci per l'architettura x86 e 28.192.048 bucket per le architetture x64 e IA-64.

Raramente la modifica di tali opzioni consente di ottenere prestazioni migliori. È possibile, ad esempio, ridurre le dimensioni della cache dei risultati del controllo dell'accesso se viene utilizzata una quantità eccessiva di memoria. In alternativa, è possibile aumentare le dimensioni della cache dei risultati del controllo dell'accesso se si verifica un utilizzo elevato della CPU quando le autorizzazioni vengono ricalcolate.

> [!IMPORTANT]
> È consigliabile modificare le opzioni solo se suggerito dal Servizio Supporto Tecnico Clienti Microsoft.
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
