---
title: Finestra di comando
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26306f8ad2adf01ebdcbf1b52169f1c2ec964920
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243078"
---
# <a name="command-window"></a>Finestra di comando
  Usare **finestra** per eseguire comandi, ad esempio comandi di debug e di modifica, sul codice nella finestra [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] dell'editor di query di cui è in corso il debug. Per usare la funzionalità **Finestra di comando**, è necessario usare la modalità di debug. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta molti dei comandi supportati anche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** window. Per altre informazioni, vedere [Visual Studio Command Window](https://go.microsoft.com/fwlink/?LinkId=112007)(Finestra di comando di Visual Studio).  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla finestra di comando**  
  
-   Scegliere **Avvia debug**dal menu **debug** .  
  
 **Per stampare il valore di una variabile**  
  
-   In **finestra**digitare **debug. Print \<VariableName>**, quindi premere INVIO.  
  
 **Per elencare le informazioni sul thread corrente**  
  
-   In **finestra**Digitare `Debug.ListThread`e quindi premere INVIO.  
  
 **Per aggiungere una variabile alla finestra controllo immediato**  
  
-   In **finestra**digitare **debug. controllo immediato \<VariableName>**, quindi premere INVIO.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](transact-sql-debugger.md)  
