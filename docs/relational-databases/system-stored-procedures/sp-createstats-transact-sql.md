---
title: sp_createstats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_createstats_TSQL
- sp_createstats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_createstats
ms.assetid: 8204f6f2-5704-40a7-8d51-43fc832eeb54
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0bb7d109323f4eb4a33181ab45b4b17d15faf54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108608"
---
# <a name="spcreatestats-transact-sql"></a>sp_createstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Chiama il [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) istruzione per creare statistiche a colonna singola su colonne che non sono già la prima colonna in un oggetto statistiche. La creazione di statistiche di colonna singola aumenta il numero di istogrammi, con un conseguente miglioramento delle stime della cardinalità, dei piani di query e delle prestazioni di esecuzione delle query. La prima colonna di un oggetto statistiche include un istogramma, mentre le altre colonne non dispongono istogrammi.  
  
 sp_createstats è utile per applicazioni quali quelle di benchmarking quando l'ora di esecuzione delle query è critica e non è possibile attendere la generazione delle statistiche di colonna singola da parte di Query Optimizer. Nella maggior parte dei casi, non è necessario utilizzare sp_createstats; i piani di query optimizer genera le statistiche a colonna singola necessarie per migliorare la query quando la **AUTO_CREATE_STATISTICS** opzione è abilitata.  
  
 Per altre informazioni sulle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md). Per altre informazioni sulla generazione di statistiche a colonna singola, vedere la **AUTO_CREATE_STATISTICS** opzione [opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_createstats   
    [   [ @indexonly =   ] { 'indexonly'   | 'NO' } ]   
    [ , [ @fullscan =    ] { 'fullscan'    | 'NO' } ]   
    [ , [ @norecompute = ] { 'norecompute' | 'NO' } ]  
    [ , [ @incremental = ] { 'incremental' | 'NO' } ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @indexonly = ] 'indexonly'` Crea statistiche solo sulle colonne in un indice esistente e non sono prime colonne in una definizione dell'indice. **indexonly** viene **char(9)** . e il valore predefinito è NO.  
  
`[ @fullscan = ] 'fullscan'` Usa il [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) istruzione con il **FULLSCAN** opzione. **FULLSCAN** viene **char(9)** .  e il valore predefinito è NO.  
  
`[ @norecompute = ] 'norecompute'` Usa il [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) istruzione con il **NORECOMPUTE** opzione. **NORECOMPUTE** viene **char(12)** .  e il valore predefinito è NO.  
  
`[ @incremental = ] 'incremental'` Usa il [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) istruzione con il **INCREMENTAL = ON** opzione. **Incrementale** viene **char(12)** .  e il valore predefinito è NO.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Il nome dei nuovi oggetti statistiche corrisponde a quello delle colonne su cui sono stati creati.  
  
## <a name="remarks"></a>Note  
 sp_createstats non crea né Aggiorna statistiche su colonne che sono prime colonne in un oggetto statistiche esistente.  Ciò include la prima colonna di statistiche create per indici, colonne con statistiche a colonna singola generate con l'opzione AUTO_CREATE_STATISTICS e la prima colonna di statistiche create con l'istruzione CREATE STATISTICS. sp_createstats non crea statistiche sulle prime colonne di indici disabilitati, a meno che tale colonna viene utilizzata in un altro indice abilitato. sp_createstats non crea statistiche sulle tabelle con un indice cluster disabilitato.  
  
 Quando la tabella contiene un set di colonne, sp_createstats non crea statistiche sulle colonne di tipo sparse. Per altre informazioni sui set di colonne e colonne di tipo sparse, vedere [utilizzare set di colonne](../../relational-databases/tables/use-column-sets.md) e [usare le colonne di tipo Sparse](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-create-single-column-statistics-on-all-eligible-columns"></a>R. Creazione di statistiche di colonna singola su tutte le colonne idonee  
 Nell'esempio seguente vengono create statistiche di colonna singola su tutte le colonne idonee del database corrente.  
  
```  
EXEC sp_createstats;  
GO  
```  
  
### <a name="b-create-single-column-statistics-on-all-eligible-index-columns"></a>B. Creazione di statistiche di colonna singola su tutte le colonne di indice idonee  
 Nell'esempio seguente vengono create statistiche di colonna singola su tutte le colonne idonee già presenti in un indice e che non sono prime colonne dell'indice.  
  
```  
EXEC sp_createstats 'indexonly';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Statistiche](../../relational-databases/statistics/statistics.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
