---
description: Messaggi restituiti dal driver ODBC per Oracle
title: Messaggi restituiti dal driver ODBC per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90f6ed20dfa954925b94e212c172ba9b69ef9596
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412477"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Messaggi restituiti dal driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Se è disponibile un messaggio di errore Oracle, verrà restituito preceduto dai tag [Microsoft], [driver ODBC per Oracle] e [Oracle]; in caso contrario, il messaggio viene restituito senza il tag [Oracle] come negli esempi seguenti:  
  
## <a name="oracle-error-message"></a>Messaggio di errore Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Messaggio di errore driver ODBC per Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
