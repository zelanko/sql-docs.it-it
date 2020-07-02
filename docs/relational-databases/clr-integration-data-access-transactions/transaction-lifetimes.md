---
title: Durate delle transazioni | Microsoft Docs
description: Informazioni sulle durate delle transazioni in SQL Server l'integrazione con CLR. Le transazioni avviate nelle stored procedure Transact-SQL sono diverse da quelle avviate nel codice gestito.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- lifetimes [SQL Server]
- Transact-SQL vs. managed code
ms.assetid: cb076fda-6488-4959-a6a4-7adaccf3f25c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a9783922f2e1e908ee13efb97512b4c16135341
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765392"
---
# <a name="transaction-lifetimes"></a>Durata delle transazioni
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Vi è un'importante differenza tra le transazioni avviate nelle stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] e quelle avviate in codice gestito: il codice CLR (Common Language Runtime) non può sbilanciare lo stato della transazione all'immissione o all'uscita di una chiamata CLR. Tenere presenti le implicazioni seguenti correlate a questa differenza:  
  
-   È necessario eseguire il commit o il rollback di una transazione avviata all'interno di un frame CLR. In caso contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un errore quando si esce dal frame.  
  
-   Non è possibile eseguire il commit o il rollback di una transazione esterna all'interno del codice CLR.  
  
-   Un tentativo di esecuzione del commit di una transazione non avviato nella stessa procedura provoca un errore di runtime.  
  
-   Il tentativo di eseguire il rollback di una transazione non avviata nella stessa procedura comporta l'interruzione della risposta da parte della transazione, evitando che si verifichino altre operazioni di effetto collaterale. La transazione viene interrotta fino a quando il codice CLR non abbandona l'ambito. Si noti che questo comportamento può risultare utile quando si rileva un errore all'interno della procedura e si desidera verificare che venga terminata l'intera transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione con CLR e transazioni](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
