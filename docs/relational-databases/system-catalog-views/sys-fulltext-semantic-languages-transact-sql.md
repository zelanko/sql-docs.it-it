---
title: sys. fulltext_semantic_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: c060f08ff70e04a22af1eb9de09aeb1e3bf4ff71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133781"
---
# <a name="sysfulltext_semantic_languages-transact-sql"></a>sys.fulltext_semantic_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni lingua il cui modello delle statistiche è registrato con l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando un modello di lingua è registrato, la lingua è abilitata per l'indicizzazione semantica.  
  
 Questa vista del catalogo è simile a [sys. fulltext_languages &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
    
||||  
|-|-|-|  
|**Nome colonna**|**Tipo**|**Descrizione**|  
|lcid|INT|ID delle impostazioni locali (LCID) di Microsoft Windows per la lingua.|  
|name|sysname|Valore dell'alias in [sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) corrispondente al valore di **LCID**o alla rappresentazione di stringa dell'identificatore LCID numerico.|  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Per altre informazioni, vedere [Installazione e configurazione della ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadati  
 Per ulteriori informazioni sul database di statistiche lingua semantica installato per supportare l'indicizzazione semantica, eseguire una query sulla vista del catalogo [sys. fulltext_semantic_language_statistics_database &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Autorizzazioni  
 La visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come eseguire una query su **sys. fulltext_semantic_languages** per ottenere informazioni su tutti i modelli di lingua registrati per l'indicizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]semantica nell'istanza corrente di.  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Installare e configurare la ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
