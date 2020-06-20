---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: rothja
ms.author: jroth
ms.openlocfilehash: a61e80867abb8ecb4d2628b74dc9956051c8e4ce
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022393"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta aggiornamento a catena ed esegue l'eliminazione tramite il meccanismo dei vincoli della chiave esterna. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_CASCADE per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione CASCADE viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_NO_ACTION per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione NO ACTION viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY.  
  
 Quando sono presenti valori non validi in un parametro **SQLForeignKeys** , **SQLForeignKeys** restituisce SQL_SUCCESS in fase di esecuzione. **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLForeignKeys** può essere eseguito su un cursore del server statico. Il tentativo di eseguire **SQLForeignKeys** su un cursore aggiornabile (dinamico o keyset) restituisce SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per i parametri *FKCatalogName* e *PKCatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLForeignKeys (funzione)](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
