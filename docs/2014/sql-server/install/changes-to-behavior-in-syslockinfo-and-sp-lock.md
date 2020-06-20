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
ms.openlocfilehash: 65ace190004cab911dd8996642720620eba94935
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045158"
---
# <a name="changes-to-behavior-in-syslockinfo-and-sp_lock"></a>Modifiche al comportamento in syslockinfo e sp_lock
  **syslockinfo** e **sp_lock** possono restituire valori imprevisti. Possono inoltre restituire righe aggiuntive, mentre le versioni precedenti di **syslockinfo** e **sp_lock** hanno restituito un massimo di due righe per ogni risorsa di blocco.  
  
 Per accedere alle informazioni da **syslockinfo** o Execute **sp_lock** è necessaria l'autorizzazione View Server state per il server.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] le colonne **rsc_objid** e **rsc_indid** in **syslockinfo** e **objid** e le colonne **indid** in **sp_lock** restituiscono in modo coerente l'ID oggetto e l'ID dell'indice. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è possibile che venga restituito il valore 0.  
  
 In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] , **syslockinfo** e **sp_lock** restituiscono un massimo di due righe per ogni risorsa di blocco specificata in una singola transazione. A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], quando il partizionamento dei blocchi è abilitato, è possibile che vengano restituite più righe per la stessa risorsa eseguita in una transazione. È possibile che vengano restituite fino a N + 1 righe, dove N è il numero di CPU. È inoltre possibile che vengano visualizzate richieste GRANTED e WAITING per la stessa risorsa, il che non è possibile in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
