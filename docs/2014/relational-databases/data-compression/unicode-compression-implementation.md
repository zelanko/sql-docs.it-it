---
title: Implementazione della compressione Unicode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a43a437b277c0fcc090a4ebd52d9deb14bec9fd0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756023"
---
# <a name="unicode-compression-implementation"></a>Implementazione della compressione Unicode
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa un'implementazione dell'algoritmo SCSU (Standard Compression Scheme for Unicode) per comprimere i valori Unicode archiviati in oggetti compressi di riga o pagina. Per questi oggetti compressi, la compressione Unicode è automatica per le colonne `nchar(n)` e `nvarchar(n)`. [!INCLUDE[ssDE](../../includes/ssde-md.md)] archivia i dati Unicode come 2 byte, indipendentemente dalle impostazioni locali. Questa funzionalità è nota come codifica UCS-2. Per alcune impostazioni locali, l'implementazione della compressione SCSU in SQL Server consente di risparmiare fino al 50 percento di spazio di archiviazione.  
  
## <a name="supported-data-types"></a>Tipi di dati supportati  
 La compressione Unicode supporta i tipi di dati a lunghezza fissa `nchar(n)` e `nvarchar(n)`. I valori di dati archiviati all'esterno di righe o in colonne `nvarchar(max)` non sono compressi.  
  
> [!NOTE]  
>  La compressione Unicode non è supportata per i dati `nvarchar(max)` anche archiviati nella riga. Questo tipo di dati, tuttavia, può ancora trarre vantaggio dalla compressione pagina.  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>Aggiornamento da versioni precedenti di SQL Server  
 Quando un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene aggiornato a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], le modifiche legate alla compressione Unicode non vengono apportate ad alcun oggetto di database, compresso o meno. Una volta aggiornato il database, gli effetti sugli oggetti sono i seguenti:  
  
-   Se l'oggetto non è compresso, non viene apportata alcuna modifica e l'oggetto continua a funzionare come in precedenza.  
  
-   Gli oggetti sui quali è stata applicata la compressione di riga o di pagina continuano a funzionare come in precedenza. I dati non compressi restano in formato non compresso finché non viene aggiornato il loro valore.  
  
-   Le nuove righe inserite in una tabella sulla quale sia stata applicata la compressione di riga o di pagina vengono compresse utilizzando la compressione Unicode.  
  
    > [!NOTE]  
    >  Per sfruttare a pieno i vantaggi della compressione Unicode, l'oggetto deve essere ricompilato con la compressione di pagina o di riga.  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Influenza della compressione Unicode sull'archiviazione dei dati  
 Quando un indice viene creato o ricompilato, oppure quando un valore viene modificato in una tabella compressa con compressione di riga o di pagina, l'indice o il valore interessato viene archiviato compresso solo se la sua dimensione compressa è inferiore alla dimensione corrente. Ciò impedisce che le dimensioni delle righe in una tabella o in un indice aumentino a causa della compressione Unicode.  
  
 Lo spazio di archiviazione risparmiato grazie alla compressione dipende dalle caratteristiche dei dati che si stanno comprimendo e dalle impostazioni locali dei dati. La seguente tabella elenca i risparmi possibili in termini di spazio per diverse impostazioni locali.  
  
|Impostazioni locali|Percentuale di compressione|  
|------------|-------------------------|  
|Inglese|50%|  
|Tedesco|50%|  
|Hindi|50%|  
|Turco|48%|  
|Vietnamita|39%|  
|Giapponese|15%|  
  
## <a name="see-also"></a>Vedere anche  
 [Compressione dei dati](data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql)   
 [Implementazione della compressione di pagina](page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql)  
  
  
