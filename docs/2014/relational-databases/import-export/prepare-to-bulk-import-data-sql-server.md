---
title: Prepararsi all'importazione bulk dei dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 03d45d9c79082b255e9b8b0e4804c50855a3ad7b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050427"
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>Prepararsi all'importazione bulk dei dati (SQL Server)
  Per importare dati in blocco solo da un file di dati, è possibile usare il comando **bcp** , l'istruzione BULK INSERT o la funzione OPENROWSET (BULK).  
  
> [!NOTE]  
>  È possibile scrivere un'applicazione personalizzata che esegua l'importazione bulk di dati da oggetti diversi da un file di testo. Per importare dati in blocco dai buffer della memoria, usare le estensioni bcp dell'interfaccia API (Application Programming Interface) Native Client (ODBC) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dell'interfaccia **IRowsetFastLoad** di OLE DB.  Per importare dati in blocco da una tabella dati C#, usare l'API della copia bulk ADO.NET, **SqlBulkCopy**.  
  
> [!NOTE]  
>  L'importazione bulk di dati in una tabella remota non è supportata.  
  
 Quando si esegue un'importazione bulk di dati da un file di dati in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], attenersi alle linee guida seguenti:  
  
-   Ottenere le autorizzazioni necessarie per l'account utente in uso.  
  
     L'account utente usato per l'esecuzione dell'utilità **bcp**, dell'istruzione BULK INSERT oppure dell'istruzione INSERT ... L'istruzione SELECT * FROM OPENROWSET(BULK...) deve disporre delle autorizzazioni necessarie per la tabella, che vengono assegnate dal proprietario della tabella. Per altre informazioni sulle autorizzazioni necessarie per ogni metodo, vedere [Utilità bcp](../../tools/bcp-utility.md), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)e [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
-   Utilizzare il modello di recupero con registrazione minima delle operazioni bulk.  
  
     Questa linea guida riguarda un database che utilizza il modello di recupero con registrazione completa. Il modello di recupero con registrazione minima delle operazioni bulk risulta utile quando si eseguono operazioni bulk in una tabella non indicizzata (un *heap*). L'utilizzo del recupero con registrazione minima delle operazioni bulk consente di evitare i problemi di esaurimento dello spazio da parte del log delle transazioni in quanto questo tipo di recupero non inserisce righe nel log. Per altre informazioni sul modello di recupero con registrazione minima delle operazioni bulk, vedere [Modelli di recupero &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md).  
  
     È consigliabile modificare il database in modo da utilizzare il modello di recupero con registrazione minima delle operazioni bulk immediatamente prima dell'operazione di importazione bulk. Appena terminata l'operazione, reimpostare il modello di recupero con registrazione completa. Per altre informazioni, vedere [Visualizzazione o modifica del modello di recupero di un database &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
    > [!NOTE]  
    >  Per altre informazioni sulla limitazione della registrazione durante le operazioni di importazione in blocco, vedere [Prerequisiti per la registrazione minima nell'importazione in blocco](prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   Eseguire il backup dopo l'importazione bulk dei dati.  
  
     Per un database che utilizza il modello di recupero con registrazione minima, è consigliabile eseguire un backup completo o differenziale al termine dell'operazione di importazione bulk. Per altre informazioni, vedere [Creare un backup completo del database &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md) o [Creare un backup differenziale del database &#40;SQL Server&#41;](../backup-restore/create-a-differential-database-backup-sql-server.md).  
  
     Per il modello di recupero con registrazione minima delle operazioni bulk o con registrazione completa, è sufficiente un backup del log. Per altre informazioni, vedere [Backup di log delle transazioni &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md).  
  
-   Eliminare gli indici della tabella al fine di migliorare le prestazioni per le importazioni bulk di grandi dimensioni.  
  
     Questa linea guida riguarda i casi in cui viene importata una grande quantità di dati rispetto alla quantità di dati già presente nella tabella. In tal caso, l'eliminazione degli indici della tabella prima dell'operazione di importazione bulk può consentire un notevole miglioramento delle prestazioni.  
  
    > [!NOTE]  
    >  Se si sta caricando una quantità di dati ridotta rispetto a quella già presente nella tabella, l'eliminazione degli indici risulta controproducente. Il tempo necessario per ricompilare gli indici potrebbe essere superiore a quello risparmiato durante l'operazione di importazione bulk.  
  
-   Individuare e rimuovere i caratteri nascosti nel file di dati.  
  
     In molte utilità ed editor di testo vengono visualizzati i caratteri nascosti, che in genere sono presenti nella parte finale del file di dati. Durante un'operazione di importazione bulk, i caratteri nascosti in un file di dati ASCII possono causare problemi che generano un errore di tipo carattere NULL imprevisto. L'individuazione e la rimozione di tutti i caratteri nascosti dovrebbero consentire di risolvere questo problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Importare ed esportare dati per operazioni bulk usando l'utilità bcp &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [Importazione di dati per operazioni bulk utilizzando BULK INSERT o OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Formati di dati per l'importazione o l'esportazione bulk &#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
