---
description: sp_prepexecrpc (Transact-SQL)
title: sp_prepexecrpc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9db0c4450f6726d39934afac27c3306dae9ded3f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535015"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Prepara ed esegue una chiamata della stored procedure con parametri specificata utilizzando un identificatore RPC. sp_prepexecrpc viene richiamato da ID = 14 in un pacchetto del flusso TDS (Tabular Data Stream).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *gestire*  
 Identificatore dell'handle preparato generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *handle* è un parametro obbligatorio con un valore restituito **int** .  
  
 *RPCCall*  
 Definisce la chiamata della stored procedure mediante la sintassi canonica ODBC. *RPCCall* è un parametro obbligatorio che richiede un valore di input di stringa **ntext** .  
  
 *bound_param*  
 Indica l'utilizzo facoltativo di parametri aggiuntivi. *bound_param* chiama un valore di input di qualsiasi tipo di dati per definire i parametri aggiuntivi in uso.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
