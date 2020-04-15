---
title: Revoca e concessione di diritti quando si utilizzano stored procedure Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303987"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revoca e concessione dei diritti durante l'uso delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver Microsoft ODBC per Oracle restituisce il seguente messaggio di errore quando i diritti utente vengono concessi e quindi revocati su una tabella a cui accede una stored procedure:  
  
 SQL_ERROR 1 AL NUMERO 1  
  
 szErrorMsg"[Microsoft][Driver ODBC per Oracle]Numero errato di parametri"  
  
 szErrorMsg"[Microsoft][Driver ODBC per Oracle]Errore di sintassi o violazione di accesso"  
  
 La chiamata alla funzione Oracle OCI Odessp() ha esito negativo in questo scenario, ma è necessaria per implementare i parametri predefiniti. Dopo la modifica delle autorizzazioni della tabella sottostante, è necessario ricompilare la stored procedure prima di eseguirla nuovamente.
