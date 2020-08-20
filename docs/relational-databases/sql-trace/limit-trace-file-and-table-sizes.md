---
description: Limitare le dimensioni di file di traccia e tabelle
title: Limitare le dimensioni di file di traccia e tabelle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- traces [SQL Server], file size
- size [SQL Server], tables
- file rollover option [SQL Server]
- size [SQL Server], files
ms.assetid: 88c31b02-f44c-4a14-be8b-437f2097de12
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2c455930e6adf93419dcb0d0934ca6ac7608c4c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455375"
---
# <a name="limit-trace-file-and-table-sizes"></a>Limitare le dimensioni di file di traccia e tabelle
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Le dimensioni dei risultati di Traccia SQL variano a seconda delle classi di evento incluse nella traccia e della modalità di utilizzo di [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se si tracciano classi di evento che si verificano di frequente, è possibile ridurre al minimo la quantità di dati raccolti dalla traccia impostando le dimensioni massime del file o il numero massimo di righe. La specifica delle dimensioni massime del file o del numero massimo di righe consente di garantire che il file o la tabella di traccia non raggiungano dimensioni superiori al limite specificato.  
  
> [!NOTE]  
>  Se i dati di traccia vengono salvati in un file già esistente, è possibile aggiungere i dati al file o sovrascriverlo. Se si sceglie di aggiungere i dati al file e le dimensioni del file di traccia sono già maggiori o uguali al valore massimo specificato, viene visualizzato un messaggio che richiede se si desidera aumentare le dimensioni massime del file o creare un nuovo file. Il meccanismo è uguale per le tabelle di traccia.  
  
## <a name="maximum-file-size"></a>Massima dimensione di file  
 Se per una traccia vengono impostate le dimensioni massime del file, il salvataggio delle informazioni nel file di traccia viene arrestato dopo il raggiungimento delle dimensioni massime. Questa opzione consente di raggruppare gli eventi in file di dimensioni inferiori e quindi più gestibili. Limitando le dimensioni del file sarà inoltre possibile eseguire in maggior sicurezza tracce automatiche, in quanto la traccia viene arrestata al raggiungimento della dimensione massima del file. È possibile impostare le dimensioni massime del file per tracce create tramite stored procedure Transact-SQL oppure [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 È previsto un limite superiore di 1 GB per le dimensioni massime del file. Il valore predefinito per le dimensioni massime del file è pari a 5 megabyte (MB).  
  
### <a name="enabling-file-rollover"></a>Abilitazione del rollover dei file  
 Quando il file corrente raggiunge le dimensioni massime, l'opzione di rollover determina la chiusura di tale file in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la creazione di un nuovo file. Il nome del nuovo file è uguale a quello del file precedente seguito da un numero intero a indicarne la sequenza. Se, ad esempio, il nome del file di traccia originale è filename_1.trc, quello del file successivo sarà filename_2.trc e così via. Se il nome assegnato a un nuovo file di rollover è già utilizzato da un file esistente, quest'ultimo verrà sovrascritto a meno che non sia di sola lettura. L'opzione di rollover dei file viene abilitata per impostazione predefinita quando si salvano i dati di traccia in un file.  
  
> [!NOTE]  
>  Con l'opzione di rollover dei file attivata, la traccia continua fino a quando non viene arrestata in qualche altro modo. Per arrestare la traccia dopo che è stato raggiunto il limite delle dimensioni del file, disabilitare l'opzione di rollover.  
  
 **Per impostare le dimensioni massime di un file di traccia**  
  
 [Impostare le dimensioni massime di un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
## <a name="maximum-number-of-rows"></a>Numero massimo di righe  
 Se per una traccia viene impostato il numero massimo di righe, il salvataggio delle informazioni in una tabella viene arrestato dopo il raggiungimento del numero massimo di righe. Ciascuna riga corrisponde a un evento, pertanto questo parametro consente di impostare un limite per il numero di eventi raccolti. L'impostazione del numero massimo di righe semplifica l'esecuzione di tracce automatiche. Se ad esempio si desidera avviare una traccia che salvi i dati di traccia in una tabella, ma si desidera arrestare la traccia qualora la tabella diventasse troppo estesa, è possibile eseguire questa operazione automaticamente.  
  
 Quando viene raggiunto il numero massimo di righe specificato, l'esecuzione della traccia proseguirà durante l'esecuzione di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , tuttavia le informazioni sulla traccia non verranno più registrate. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] continua a visualizzare i risultati della traccia fino all'arresto della traccia.  
  
 **Per impostare il numero massimo di righe di una traccia**  
  
 [Impostare le dimensioni massime di un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
## <a name="see-also"></a>Vedere anche  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)  
  
  
