---
description: Configurazione e gestione di filtri per la ricerca
title: Configurare e gestire filtri per la ricerca | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ebeaebbc4a082bcb7051dc3d6c784b6ce1ec11fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420355"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurazione e gestione di filtri per la ricerca
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  L'indicizzazione di un documento in una colonna con tipo di dati **varbinary**, **varbinary(max)**, **image** o **xml** richiede operazioni di elaborazione aggiuntive. che devono essere eseguite mediante un filtro. Il filtro estrae le informazioni testuali dal documento rimuovendo la formattazione, quindi invia il testo al word breaker per la lingua associata alla colonna della tabella.  
 
## <a name="filters-and-document-types"></a>Filtri e tipi di documento
Un determinato filtro è specifico di un determinato tipo di documento (file con estensione doc, pdf, xls, xml e così via). Questi filtri implementano l'interfaccia IFilter. Per altre informazioni su questi tipi di documento, eseguire una query nella vista del catalogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
I documenti binari possono essere archiviati in una singola colonna **varbinary(max)** o **image** . Per ogni documento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sceglie il filtro corretto da utilizzare in base all'estensione file. Considerato che l'estensione non è visibile quando il file viene archiviato in una colonna **varbinary(max)** o **image** , l'estensione file (DOC, XLS, PDF e così via) deve essere archiviata in una colonna distinta della tabella, denominata colonna del tipo. Questa colonna può includere qualsiasi tipo di dati basato su caratteri e contiene l'estensione file del documento, ad esempio l'estensione doc per un documento di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. Nella tabella **Document** in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]la colonna **Document** è di tipo **varbinary(max)** mentre la colonna del tipo, **FileExtension**, è di tipo **nvarchar(8)**.  

**Per visualizzare la colonna del tipo in un indice full-text esistente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  Un filtro potrebbe essere in grado di gestire gli oggetti incorporati nell'oggetto padre, a seconda della relativa implementazione. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tuttavia, i filtri non vengono configurati per seguire collegamenti ad altri oggetti.  

## <a name="installed-filters"></a>Filtri installati 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installa i propri filtri XML e HTML. Anche gli eventuali filtri per i formati proprietari [!INCLUDE[msCoName](../../includes/msconame-md.md)] (con estensione doc, xdoc, ppt e così via) già installati nel sistema operativo vengono caricati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per identificare i filtri attualmente caricati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usare la stored procedure [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) nel modo seguente:  

```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  

> [!NOTE]
> Anche con la versione più recente di Office Filter Pack che offre il supporto dell'estensione xlsx, SQL Server non supporta i fogli di calcolo Strict Open XML.  Non verrà restituito alcun errore, ma SQL Server non riuscirà a indicizzare alcun contenuto dei fogli di calcolo di tipo Strict Open XML.

## <a name="non-microsoft-filters"></a>Filtri non Microsoft
Per poter usare i filtri per formati non [!INCLUDE[msCoName](../../includes/msconame-md.md)], è tuttavia necessario caricarli manualmente nell'istanza del server. Per informazioni sull'installazione di filtri aggiuntivi, vedere [Visualizzare o modificare word breaker e filtri registrati](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilità FILESTREAM con altre funzionalità di SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
