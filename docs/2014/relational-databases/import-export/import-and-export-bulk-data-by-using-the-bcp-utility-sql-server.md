---
title: Importare ed esportare dati per operazioni bulk usando l'utilità bcp (SQL Server) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 06/14/2017
ms.openlocfilehash: 7075bf87ed64686750bc4a267af431268987ff35
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708216"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importazione ed esportazione di dati per operazioni bulk tramite l'utilità bcp (SQL Server)

Questo argomento offre una panoramica sull'uso dell'[utilità bcp](../../tools/bcp-utility.md) per l'esportazione di dati da qualsiasi posizione di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è possibile usare un'istruzione SELECT, incluse le viste partizionate.  
  
 L'utilità bcp (Bcp.exe) è uno strumento della riga di comando che utilizza l'API del programma per la copia bulk (BCP). L'utilità bcp consente di eseguire le operazioni seguenti:  
  
-   Esportazioni bulk di dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati.  
  
-   Esportazioni bulk di dati da una query.  
  
-   Importazioni bulk di dati da un file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Generazione di file di formato.  
  
 L'utilità bcp è accessibile con il comando **bcp** . Per usare il comando **bcp** un'importazione in blocco di dati, è necessario conoscere lo schema della tabella e i tipi di dati delle colonne, a meno che non venga usato un file di formato preesistente.  
  
 L'utilità consente di esportare dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati per utilizzarli in altri programmi. Consente inoltre di importare dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un altro programma, in genere un altro sistema di gestione di database (DBMS, Database Management System). I dati vengono innanzitutto esportati dal programma di origine in un file di dati e quindi, in un'operazione separata, vengono copiati dal file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Le opzioni del comando **bcp** consentono di specificare il tipo di dati del file di dati e altre informazioni. Se tali opzioni non vengono specificate, verrà richiesto di immettere le informazioni sulla formattazione, ad esempio il tipo dei campi dati di un file di dati. Verrà quindi richiesto se si desidera creare un file di formato contenente le risposte interattive fornite. Un file di formato risulta spesso utile per assicurare la flessibilità per operazioni future di importazione o esportazione bulk. È possibile specificare il file di formato in comandi **bcp** successivi per file di dati equivalenti. Per altre informazioni, vedere [Specificare i formati di dati per la compatibilità con bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  L'utilità bcp è scritta tramite la copia bulk di ODBC  
  
 Per una descrizione della sintassi del comando **bcp**, vedere [Utilità bcp](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Esempi

 Per esempi su **bcp**, vedere:  
  
-   [Utilità bcp](../../tools/bcp-utility.md)  
  
-   [Creare un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Specificare caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Utilizzo di un file di formato per l'importazione bulk dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usare il formato carattere per importare o esportare dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato carattere Unicode per importare o esportare dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  

## <a name="see-also"></a>Vedere anche

[Insert &#40;Transact-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql)
[clausola &#40;SELECT Transact-SQL&#41; ](/sql/t-sql/queries/select-clause-transact-sql)
[utilità bcp](../../tools/bcp-utility.md)   
[Preparare l'importazione bulk dei &#40;dati&#41; SQL Server](prepare-to-bulk-import-data-sql-server.md)
[Bulk Insert &#40;Transact-&#41; SQL](/sql/t-sql/statements/bulk-insert-transact-sql)
eseguire l' [importazione e l' &#40;esportazione&#41; bulk dei dati SQL Server](bulk-import-and-export-of-data-sql-server.md)
[OPENROWSET &#40;Transact-SQL&#41; ](/sql/t-sql/functions/openrowset-transact-sql)
[creare un file &#40;di formato SQL Server&#41; ](create-a-format-file-sql-server.md)