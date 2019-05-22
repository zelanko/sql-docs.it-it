---
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6aca3cf59d386dc9913103d69d00dc3ecb973283
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982990"
---
# <a name="spfulltextsemanticunregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di annullare la registrazione di un database di statistiche lingua semantica esistente dall'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di eliminare tutti i metadati associati.  
  
 Questa istruzione non consente di scollegare il database o di rimuovere il file di database fisico dal file system. Dopo avere annullato la registrazione del database, è possibile scollegarlo ed eliminare il file di database fisico.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="Arguments"></a> Argomenti  
 In questa procedura non è necessario utilizzare alcun argomento. Poiché un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include un solo database di statistiche lingua semantica, non è necessario identificare il database.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-set"></a>Set di risultati  
 Nessuna.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Quando si annulla la registrazione di un database di statistiche lingua semantica, vengono rimossi anche tutti i metadati associati.  
  
 **sp_fulltext_semantic_unregister_language_statistics_db** esegue i passaggi seguenti:  
  
1.  Verificare che non vi sia in corso alcun popolamento semantico per l'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Rimuovere tutti i metadati associati al database di statistiche lingua semantica.  
  
 Per altre informazioni, vedere [Installazione e configurazione della ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadati  
 Per informazioni sul database di statistiche lingua semantica installato in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire una query sulla vista del catalogo [Sys. fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 Sono necessarie autorizzazioni CONTROL SERVER.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come annullare la registrazione del database di statistiche lingua semantica chiamando **sp_fulltext_semantic_unregister_language_statistics_db**.  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Installare e configurare la ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
