---
title: SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTablePrivileges function
ms.assetid: 8cce22d5-28b1-4b50-a5bc-1de03e0ffd6b
author: rothja
ms.author: jroth
ms.openlocfilehash: 63298330d3f0ebf707dbb42c337553c1f363deab
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021435"
---
# <a name="sqltableprivileges"></a>SQLTablePrivileges
  **SQLTablePrivileges** può essere eseguito su un cursore statico. Un tentativo di eseguire **SQLTablePrivileges** su un oggetto aggiornabile (gestito da keyset o dinamico) restituisce SQL_SUCCESS_WITH_INFO indicante che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTablePrivileges] (https://go.microsoft.com/fwlink/?LinkId=59373\)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
