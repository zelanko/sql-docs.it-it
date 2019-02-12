---
title: sys.dm_repl_articles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 65bc88be1b9a6cdb9a69d41a526916ab3aa7ab2a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031832"
---
# <a name="sysdmreplarticles-transact-sql"></a>sys.dm_repl_articles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli oggetti di database pubblicati come articoli in una topologia di replica.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary(8)**|Indirizzo in memoria della struttura di database nella cache per il database di pubblicazione.|  
|**artcache_table_address**|**varbinary(8)**|Indirizzo in memoria della struttura di tabella nella cache per un articolo di tabella pubblicato.|  
|**artcache_schema_address**|**varbinary(8)**|Indirizzo in memoria della struttura di schemi di articolo nella cache per un articolo di tabella pubblicato.|  
|**artcache_article_address**|**varbinary(8)**|Indirizzo in memoria della struttura di articoli nella cache per un articolo di tabella pubblicato.|  
|**artid**|**bigint**|Identificatore univoco di ogni voce nella tabella.|  
|**artfilter**|**bigint**|ID della stored procedure utilizzata per filtrare l'articolo in senso orizzontale.|  
|**artobjid**|**bigint**|ID dell'oggetto pubblicato.|  
|**artpubid**|**bigint**|ID della pubblicazione a cui appartiene l'articolo.|  
|**artstatus**|**tinyint**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = articolo è attivo.<br /><br /> **8** = Include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = utilizza istruzioni con parametrizzata.<br /><br /> **24** = entrambi includono il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri includerà il valore 17 in questa colonna. Il valore 0 indica che l'articolo è inattivo e che non sono state definite proprietà aggiuntive.|  
|**arttype**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.<br /><br /> **8** = esecuzione di Stored procedure.<br /><br /> **24** = esecuzione di stored procedure serializzabile.<br /><br /> **32** = Stored procedure (solo schema).<br /><br /> **64** = vista (solo schema).<br /><br /> **128** = function (solo schema).|  
|**wszArtdesttable**|**nvarchar(514)**|Nome dell'oggetto pubblicato nella destinazione.|  
|**wszArtdesttableowner**|**nvarchar(514)**|Proprietario dell'oggetto pubblicato nella destinazione.|  
|**wszArtinscmd**|**nvarchar(510)**|Comando o stored procedure utilizzati per gli inserimenti.|  
|**cmdTypeIns**|**int**|Sintassi della stored procedure INSERT. I possibili valori sono i seguenti.<br /><br /> **1** = CALL<br /><br /> **2** = SQL<br /><br /> **3** = NONE<br /><br /> **7** = SCONOSCIUTO|  
|**wszArtdelcmd**|**nvarchar(510)**|Comando o stored procedure utilizzati per le eliminazioni.|  
|**cmdTypeDel**|**int**|Sintassi della stored procedure DELETE. I possibili valori sono i seguenti.<br /><br /> **0** = XCALL<br /><br /> **1** = CALL<br /><br /> **2** = SQL<br /><br /> **3** = NONE<br /><br /> **7** = SCONOSCIUTO|  
|**wszArtupdcmd**|**nvarchar(510)**|Comando o stored procedure utilizzati per gli aggiornamenti.|  
|**cmdTypeUpd**|**int**|Sintassi della stored procedure UPDATE. I possibili valori sono i seguenti.<br /><br /> **0** = XCALL<br /><br /> **1** = CALL<br /><br /> **2** = SQL<br /><br /> **3** = NONE<br /><br /> **4** = MCALL<br /><br /> **5** = VCALL<br /><br /> **6** = SCALL<br /><br /> **7** = SCONOSCIUTO|  
|**wszArtpartialupdcmd**|**nvarchar(510)**|Comando o stored procedure utilizzati per gli aggiornamenti parziali.|  
|**cmdTypePartialUpd**|**int**|Sintassi della stored procedure di aggiornamento parziale. I possibili valori sono i seguenti.<br /><br /> **2** = SQL|  
|**numcol**|**int**|Numero di colonne nella partizione per un articolo filtrato in senso verticale.|  
|**artcmdtype**|**tinyint**|Tipo di comando replicato. I possibili valori sono i seguenti.<br /><br /> **1** = INSERT<br /><br /> **2** = DELETE<br /><br /> **3** = AGGIORNAMENTO<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = none<br /><br /> **6** = solo per uso interno<br /><br /> **7** = solo per uso interno<br /><br /> **8** = UPDATE parziale|  
|**artgeninscmd**|**nvarchar(510)**|Modello di comando INSERT basato sulle colonne incluse nell'articolo.|  
|**artgendelcmd**|**nvarchar(510)**|Modello di comando DELETE che può includere la chiave primaria o le colonne incluse nell'articolo, in base alla sintassi utilizzata.|  
|**artgenupdcmd**|**nvarchar(510)**|Modello di comando UPDATE che può includere la chiave primaria, le colonne aggiornate o una lista completa di colonne, in base alla sintassi utilizzata.|  
|**artpartialupdcmd**|**nvarchar(510)**|Modello di comando UPDATE parziale contenente la chiave primaria e le colonne aggiornate.|  
|**artupdtxtcmd**|**nvarchar(510)**|Modello di comando UPDATETEXT contenente la chiave primaria e le colonne aggiornate.|  
|**artgenins2cmd**|**nvarchar(510)**|Modello di comando INSERT utilizzato per la riconciliazione di un articolo durante l'elaborazione di snapshot simultanei.|  
|**artgendel2cmd**|**nvarchar(510)**|Modello di comando DELETE utilizzato per la riconciliazione di un articolo durante l'elaborazione di snapshot simultanei.|  
|**fInReconcile**|**tinyint**|Indica se un articolo verrà riconciliato durante l'elaborazione di snapshot simultanei.|  
|**fPubAllowUpdate**|**tinyint**|Indica se la pubblicazione consente sottoscrizioni aggiornabili.|  
|**intPublicationOptions**|**bigint**|Mappa di bit che specifica opzioni di pubblicazione aggiuntive. I possibili valori delle opzioni bit per bit sono i seguenti:<br /><br /> **0x1** : abilitato per la replica peer-to-peer.<br /><br /> **0x2** -pubblicare solo modifiche locali.<br /><br /> **0x4** - enabled per sottoscrittori non SQL Server.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE nel database di pubblicazione per chiamare **dm_repl_articles**.  
  
## <a name="remarks"></a>Note  
 Vengono restituite informazioni solo per gli oggetti di database replicati caricati nella cache dell'articolo di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Viste a gestione dinamica relative alle repliche &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

