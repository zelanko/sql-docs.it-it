---
title: Finestra di comando
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 226acc4696b5edacde3b6950c10c8b5370e29b42
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75243433"
---
# <a name="transact-sql-debugger---command-window"></a>Debugger Transact-SQL - Finestra di comando

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Usare la funzionalità **Finestra di comando** per eseguire comandi, ad esempio i comandi debug o di modifica, sul codice incluso nella finestra dell'editor di query del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di cui è in corso il debug. Per usare la funzionalità **Finestra di comando**, è necessario usare la modalità di debug. Il debugger [!INCLUDE[tsql](../../includes/tsql-md.md)] supporta molti dei comandi supportati anche nella finestra **Comando** di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per altre informazioni, vedere [Visual Studio Command Window](https://go.microsoft.com/fwlink/?LinkId=112007)(Finestra di comando di Visual Studio).  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>Elenco attività

**Per accedere alla funzionalità Finestra di comando**

- Scegliere **Avvia debug** dal menu **Debug**.

**Per stampare il valore di una variabile**

- In **Finestra di comando** digitare **Debug.Print \<NomeVariabile>** , quindi premere INVIO.

**Per elencare le informazioni sul thread corrente**

- In **Finestra di comando**digitare **Debug.ListThread**, quindi premere INVIO.

**Per aggiungere una variabile alla finestra Controllo immediato**

- In **Finestra di comando** digitare **Debug.QuickWatch \<NomeVariabile>** , quindi premere INVIO.

## <a name="see-also"></a>Vedere anche

[Debugger Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)
