---
title: Revoca e concessione di diritti quando si utilizzano stored procedure | Microsoft Docs
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
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987958"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>Revoca e concessione dei diritti durante l'uso delle stored procedure
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Microsoft ODBC driver for Oracle restituisce il seguente messaggio di errore quando i diritti utente vengono concessi e quindi revocati in una tabella a cui accede un stored procedure:  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [driver ODBC per Oracle] numero di parametri errato"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] errore di sintassi o violazione di accesso"  
  
 La chiamata alla funzione Oracle OCI odessp () ha esito negativo in questo scenario, ma è necessaria per implementare parametri predefiniti. Dopo la modifica delle autorizzazioni della tabella sottostante, è necessario ricompilare il stored procedure prima di eseguirlo di nuovo.
