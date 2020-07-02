---
title: Oggetto SqlTriggerContext | Microsoft Docs
description: In SQL Server integrazione con CLR, la classe SqlTriggerContext fornisce informazioni di contesto per un trigger, incluso il tipo di azione e le colonne modificate in Operation.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 4634a0c95e64516b6364fbfd68edeb9cd6156511
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765409"
---
# <a name="sqltriggercontext-object"></a>Oggetto SqlTriggerContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La classe **SqlTriggerContext** fornisce informazioni sul contesto per il trigger. Tali informazioni includono il tipo di azione che ha provocato l'attivazione del trigger, le colonne modificate in un'operazione UPDATE e, nel caso di un trigger DDL, una struttura XML **EventData** che descrive l'operazione di attivazione del trigger. Per ulteriori informazioni ed esempi su come utilizzare la classe **SqlTriggerContext** , vedere [trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
 Per ulteriori informazioni, vedere la documentazione di riferimento della classe **Microsoft. SqlServer. Server. SqlTriggerContext** nella documentazione di .NET Framework SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
