---
description: DROP SEARCH PROPERTY LIST (Transact-SQL)
title: DROP SEARCH PROPERTY LIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: de8f55242f3727eb1491b9a89e9bf7d349cef860
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131112"
---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina un elenco di proprietà dal database corrente se l'elenco delle proprietà di ricerca non è attualmente associato a un indice full-text nel database.  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *property_list_name*  
 Nome dell'elenco delle proprietà di ricerca da eliminare. *property_list_name* è un identificatore.  
  
 Per visualizzare i nomi degli elenchi delle proprietà esistenti, usare la vista del catalogo [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md), come illustrato di seguito:  
  
```sql  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>Commenti  
 Non è possibile eliminare un elenco di proprietà di ricerca da un database se l'elenco è associato a un indice full-text e i relativi tentativi avranno esito negativo. Per eliminare un elenco di proprietà di ricerca da un indice full-text specificato, usare l'istruzione [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) e specificare la clausola SET SEARCH PROPERTY LIST con OFF o il nome di un altro elenco di proprietà di ricerca.  
  
 **Per visualizzare gli elenchi di proprietà in un'istanza del server**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **Per visualizzare gli elenchi di proprietà associati a indici full-text**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **Per rimuovere un elenco di proprietà da un indice full-text**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione CONTROL per l'elenco delle proprietà di ricerca.  
  
> [!NOTE]  
>  Le autorizzazioni CONTROL possono essere concesse per l'elenco dal proprietario dell'elenco di proprietà. Per impostazione predefinita, l'utente che crea un elenco di proprietà di ricerca è il proprietario. Il proprietario può essere modificato usando l'istruzione [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eliminato l'elenco di proprietà `JobCandidateProperties` dal database `AdventureWorks2012`.  
  
```sql  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [Eseguire ricerche nelle proprietà dei documenti con elenchi delle proprietà di ricerca](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  
