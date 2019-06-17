---
title: Modifiche al comportamento in syslockinfo e sp_lock | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8c6534449ffc4e89efcd49c943726bf6ecd9f26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096651"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Modifiche al comportamento in syslockinfo e sp_lock
  **syslockinfo** e **sp_lock** possono restituire valori imprevisti. Possono inoltre restituire righe aggiuntive, mentre precedenti versioni di **syslockinfo** e **sp_lock** ha restituito un massimo di due righe per ogni risorsa di blocco.  
  
 Per accedere alle informazioni da **syslockinfo** o eseguire **sp_lock** è richiesta l'autorizzazione VIEW SERVER STATE nel server.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Nella [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], il **rsc_objid** e **rsc_indid** colonne **syslockinfo** e il **objid** e **indid**  colonne **sp_lock** restituire l'ID di oggetto in modo coerente e l'ID indice In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è possibile che venga restituito il valore 0.  
  
 Nelle [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** e **sp_lock** restituire un massimo di due righe per qualsiasi risorsa di blocco specificata in una singola transazione. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], quando il partizionamento dei blocchi è abilitato, è possibile che vengano restituite più righe per la stessa risorsa eseguita in una transazione. Si possono essere fino a N + 1 righe restituito, dove N è il numero di CPU. È inoltre possibile che vengano visualizzate richieste GRANTED e WAITING per la stessa risorsa, il che non è possibile in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
