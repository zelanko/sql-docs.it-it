---
title: Finestra di comando | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b6fd133b1a2829d366e09fc340e0b9b7bfb1ff0
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67679565"
---
# <a name="transact-sql-debugger---command-window"></a>Debugger Transact-SQL - Finestra di comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Usare la funzionalità **Finestra di comando** per eseguire comandi, ad esempio i comandi debug o di modifica, sul codice incluso nella finestra dell'editor di query del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di cui è in corso il debug. Per usare la funzionalità **Finestra di comando**, è necessario usare la modalità di debug. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta molti dei comandi supportati anche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **Command** window. Per altre informazioni, vedere [Visual Studio Command Window](https://go.microsoft.com/fwlink/?LinkId=112007)(Finestra di comando di Visual Studio).  
  
## <a name="task-list"></a>Elenco attività  
 **Per accedere alla funzionalità Finestra di comando**  
  
-   Scegliere **Avvia debug** dal menu **Debug**.  
  
 **Per stampare il valore di una variabile**  
  
-   In **Finestra di comando** digitare **Debug.Print \<NomeVariabile>** , quindi premere INVIO.  
  
 **Per elencare le informazioni sul thread corrente**  
  
-   In **Finestra di comando**digitare **Debug.ListThread**, quindi premere INVIO.  
  
 **Per aggiungere una variabile alla finestra Controllo immediato**  
  
-   In **Finestra di comando** digitare **Debug.QuickWatch \<NomeVariabile>** , quindi premere INVIO.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
