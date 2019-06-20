---
title: Revoca e concessione dei diritti di quando si utilizzano Stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e881201e4653a168faff2fa438be19c1ca37e9b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127956"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revoca e concessione dei diritti durante l'uso delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Il Driver ODBC di Microsoft per Oracle restituisce il messaggio di errore seguente quando diritti utente vengono concesse e infine revocati in una tabella a cui accede una stored procedure:  
  
 SQL_ERROR=-1  
  
 szErrorMsg = "[Microsoft] [driver ODBC per Oracle] numero errato di parametri"  
  
 szErrorMsg = "[Microsoft] [driver ODBC per Oracle] sintassi o violazione di accesso"  
  
 La chiamata alla funzione Oracle OCI Odessp() ha esito negativo in questo scenario, ma è necessaria per implementare i parametri predefiniti. Dopo che le autorizzazioni nella tabella sottostante vengono modificate, è necessario ricompilare la stored procedure prima di eseguirlo nuovamente.
