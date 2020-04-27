---
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ef8a59c98bc6669a13b5a4ffeb516b4063db23c7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915898"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1205|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LK_VICTIM|  
|Testo del messaggio|La transazione (ID di processo %d) è stata interrotta a causa di un deadlock delle risorse %.*ls con un altro processo. Ripetere la transazione.|  
  
## <a name="explanation"></a>Spiegazione  
 Accesso alle risorse in ordine conflittuale in transazioni distinte, con conseguente deadlock. Ad esempio:  
  
-   Transaction1 aggiorna **Table1.Row1**, mentre Transaction2 aggiorna **Table2.Row2**.  
  
-   Transaction1 tenta di aggiornare **Table2.Row2** ma viene bloccata perché non è ancora stato eseguito il commit di Transaction2.  
  
-   Transaction2 tenta quindi di aggiornare **Table1.Row1** ma viene bloccata perché non è stato eseguito il commit di Transaction1.  
  
-   Si verifica un deadlock perché Transaction1 è in attesa del completamento di Transaction2 e Transaction2 è in attesa a sua volta del completamento di Transaction1.  
  
 Il sistema rileva il deadlock e sceglie una delle transazioni interessate come "vittima" e genera questo messaggio. Eseguire il rollback della transazione vittima.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire nuovamente la transazione. È inoltre possibile modificare l'applicazione per evitare i deadlock. È possibile tentare di eseguire nuovamente la transazione scelta come vittima. In base alle operazioni che verranno eseguite simultaneamente, è probabile che la transazione abbia esito positivo.  
  
 Per impedire che si verifichino deadlock, è consigliabile che tutte le transazioni accedano alle righe nello stesso ordine (**Table1**, quindi **Table2**). In questo modo, sebbene sia possibile che si verifichi un blocco, non si verificherà un deadlock.  
  
  
