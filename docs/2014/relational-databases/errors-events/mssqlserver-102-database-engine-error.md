---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee88ba8a77602fd50412669f96e1e16ddcdd37c7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870739"
---
# <a name="mssqlserver_102"></a>MSSQLSERVER_102
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|102|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|P_SYNTAXERR2|  
|Testo del messaggio|Sintassi non corretta in prossimità di '%.*ls'.|  
  
## <a name="explanation"></a>Spiegazione  
 Indica un errore di sintassi. Le informazioni aggiuntive non sono disponibili perché l'errore non consente l'elaborazione dell'istruzione da parte di [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Questa situazione può essere causata dal tentativo di creare una chiave simmetrica utilizzando la crittografia deprecata RC4 o RC4_128 quando la modalità di compatibilità non è 90 o 100.  
  
## <a name="user-action"></a>Azione dell'utente  
 Ricercare errori di sintassi nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se si crea una chiave simmetrica utilizzando RC4 o RC4_128, selezionare un metodo di crittografia più recente, ad esempio uno degli algoritmi AES (opzione consigliata). Se è necessario utilizzare RC4, eseguire ALTER DATABASE SET COMPATIBILITY_LEVEL per impostare il database sul livello di compatibilità 90 o 100. (Non consigliato.)  
  
  
