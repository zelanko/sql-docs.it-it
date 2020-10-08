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
ms.openlocfilehash: c6f11eda2ef791eb8c987af8d82149507770d47a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809161"
---
# <a name="sqltriggercontext-object"></a>Oggetto SqlTriggerContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La classe **SqlTriggerContext** fornisce informazioni sul contesto per il trigger. Tali informazioni includono il tipo di azione che ha provocato l'attivazione del trigger, le colonne modificate in un'operazione UPDATE e, nel caso di un trigger DDL, una struttura XML **EventData** che descrive l'operazione di attivazione del trigger. Per ulteriori informazioni ed esempi su come utilizzare la classe **SqlTriggerContext** , vedere [trigger CLR](/dotnet/framework/data/adonet/sql/clr-triggers).  
  
 Per ulteriori informazioni, vedere la documentazione di riferimento della classe **Microsoft. SqlServer. Server. SqlTriggerContext** nella documentazione di .NET Framework SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger CLR](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
