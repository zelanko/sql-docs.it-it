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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7f8e72831e333323621279a0403e95e6a134860
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718421"
---
# <a name="command-window"></a>Finestra di comando
  Usare la funzionalità **Finestra di comando** per eseguire comandi, ad esempio i comandi debug o di modifica, sul codice incluso nella finestra dell'editor di query del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di cui è in corso il debug. Per usare la funzionalità **Finestra di comando**, è necessario usare la modalità di debug. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta molti dei comandi supportati anche nella finestra **Comando** di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per altre informazioni, vedere [Visual Studio Command Window](https://go.microsoft.com/fwlink/?LinkId=112007)(Finestra di comando di Visual Studio).  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla funzionalità Finestra di comando**  
  
-   Scegliere **Avvia debug** dal menu **Debug**.  
  
 **Per stampare il valore di una variabile**  
  
-   In **Finestra di comando** digitare **Debug.Print \<NomeVariabile>** , quindi premere INVIO.  
  
 **Per elencare le informazioni sul thread corrente**  
  
-   In **finestra**Digitare `Debug.ListThread` e quindi premere INVIO.  
  
 **Per aggiungere una variabile alla finestra Controllo immediato**  
  
-   In **Finestra di comando** digitare **Debug.QuickWatch \<NomeVariabile>** , quindi premere INVIO.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](transact-sql-debugger.md)  
