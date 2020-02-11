---
title: Funzioni deterministiche e non deterministiche | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5463ac19caf9a82e48dd59c4ba05873587b74324
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62714728"
---
# <a name="deterministic-and-nondeterministic-functions"></a>Funzioni deterministiche e non deterministiche
  Le funzioni deterministiche restituiscono sempre lo stesso risultato quando vengono chiamate con un set di valori di input specifico e se lo stato del database rimane invariato. Le funzioni non deterministiche possono restituire risultati diversi quando vengono chiamate con un set di valori di input specifico, anche se lo stato del database a cui accedono rimane invariato. Ad esempio, tramite la funzione AVG viene restituito sempre lo stesso risultato in base alle condizioni indicate in precedenza, ma tramite la funzione GETDATE, mediante la quale viene restituito il valore datetime corrente, viene sempre restituito un risultato diverso.  
  
 Le funzioni definite dall'utente includono diverse proprietà che influiscono sulla capacità del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di indicizzare i risultati della funzione, tramite gli indici nelle colonne calcolate che chiamano la funzione o tramite le viste indicizzate che fanno riferimento alla funzione. Una di queste proprietà è la proprietà deterministica di una funzione. Non è, ad esempio, possibile creare un indice cluster in una vista se la vista fa riferimento a funzioni non deterministiche. Per altre informazioni sulle proprietà delle funzioni, inclusa la proprietà deterministica, vedere [Funzioni definite dall'utente](user-defined-functions.md).  
  
 In questo argomento vengono illustrati la proprietà deterministica delle funzioni di sistema predefinite e l'effetto sulla proprietà deterministica delle funzioni definite dall'utente quando contiene una chiamata a stored procedure estese.  
  
## <a name="built-in-function-determinism"></a>Proprietà deterministica delle funzioni predefinite  
 Non è possibile influenzare la proprietà deterministica di alcuna funzione predefinita. Ogni funzione predefinita è deterministica o non deterministica in base al modo in cui viene implementata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, la specifica di una clausola ORDER BY in una query non comporta la modifica del determinismo di una funzione utilizzata nella query in questione.  
  
 Tutte le funzioni per i valori stringa predefinite sono deterministiche. Per un elenco di queste funzioni, vedere [Funzioni per i valori stringa &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql).  
  
 Le funzioni riportate di seguito, appartenenti alle categorie di funzioni predefinite diverse da quelle per i valori stringa, sono sempre deterministiche.  
  
||||  
|-|-|-|  
|abs|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|LOG|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 Le funzioni elencate di seguito non sono sempre deterministiche, ma possono essere utilizzate in viste indicizzate o indici in colonne calcolate quando vengono specificate in modo deterministico.  
  
|Funzione|Commenti|  
|--------------|--------------|  
|Tutte le funzioni di aggregazione|Tutte le funzioni di aggregazione sono deterministiche a meno che non vengano specificate con le clausole OVER e ORDER BY. Per un elenco di queste funzioni, vedere [Funzioni di aggregazione &#40;Transact-SQL&#41;](/sql/t-sql/functions/aggregate-functions-transact-sql).|  
|CAST|Deterministica a meno che non venga utilizzata con `datetime`, `smalldatetime` o `sql_variant`.|  
|CONVERT|Deterministica a meno che non si verifichi una delle condizioni seguenti:<br /><br /> Il tipo di origine è `sql_variant`.<br /><br /> Il tipo di destinazione è `sql_variant` e il relativo tipo di origine è non deterministico.<br /><br /> Il tipo di origine o di destinazione è `datetime` o `smalldatetime`, l'altro tipo di origine o di destinazione è una stringa di caratteri. Inoltre è specificato uno stile non deterministico. Per essere deterministico, il parametro di stile deve essere una costante. Gli stili minori o uguali a 100 sono non deterministici, ad eccezione degli stili 20 e 21. Gli stili maggiori di 100 sono deterministici, ad eccezione degli stili 106, 107, 109 e 113.|  
|CHECKSUM|Deterministica, ad eccezione di CHECKSUM(*).|  
|ISDATE|Deterministica solo se utilizzata con la funzione CONVERT, se è specificato il parametro di stile CONVERT e se lo stile non equivale a 0, 100, 9 o 109.|  
|RAND|RAND risulta deterministica solo quando si specifica un parametro per il *valore di inizializzazione* .|  
  
 Tutte le funzioni statistiche di sistema, di configurazione, per i cursori, per i metadati e di sicurezza sono di tipo non deterministico. Per un elenco di queste funzioni, vedere [Funzioni di configurazione &#40;Transact-SQL&#41;](/sql/t-sql/functions/configuration-functions-transact-sql), [Funzioni per i cursori &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-functions-transact-sql), [Funzioni per i metadati &#40;Transact-SQL&#41;](/sql/t-sql/functions/metadata-functions-transact-sql), [Funzioni di sicurezza &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql) e [Funzioni statistiche di sistema &#40;Transact-SQL&#41;](/sql/t-sql/functions/system-statistical-functions-transact-sql).  
  
 Di seguito sono elencate le funzioni predefinite di altre categorie che sono sempre non deterministiche.  
  
|||  
|-|-|  
|@@CONNECTIONS|GETDATE|  
|@@CPU_BUSY|GETUTCDATE|  
|@@DBTS|GET_TRANSMISSION_STATUS|  
|@@IDLE|LAG|  
|@@IO_BUSY|LAST_VALUE|  
|@@MAX_CONNECTIONS|LEAD|  
|@@PACK_RECEIVED|MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT|NEWID|  
|@@PACKET_ERRORS|NEWSEQUENTIALID|  
|@@TIMETICKS|NEXT VALUE FOR|  
|@@TOTAL_ERRORS|NTILE|  
|@@TOTAL_READ|PARSENAME|  
|@@TOTAL_WRITE|PERCENTILE_CONT|  
|CUME_DIST|PERCENTILE_DISC|  
|CURRENT_TIMESTAMP|PERCENT_RANK|  
|DENSE_RANK|RAND|  
|FIRST_VALUE|RANK|  
||ROW_NUMBER|  
||TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>Chiamata di stored procedure estese da funzioni  
 Le funzioni che chiamano stored procedure estese sono non deterministiche, in quanto le stored procedure estese possono avere effetti collaterali sul database, ovvero possono comportare modifiche di uno stato globale del database, quale un aggiornamento di una tabella o di una risorsa esterna, come un file o la rete, tramite, ad esempio, la modifica di un file o l'invio di un messaggio di posta elettronica. Quando si esegue una stored procedure estesa da una funzione definita dall'utente, il set di risultati restituito potrebbe non essere coerente. Le funzioni definite dall'utente che creano effetti collaterali sul database non sono consigliate.  
  
 Quando viene chiamata dall'interno di una funzione, una stored procedure estesa non può restituire set di risultati al client. Qualsiasi API ODS che restituisca set di risultati al client restituirà il codice FAIL.  
  
 La stored procedure estesa può connettersi nuovamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tuttavia, la procedura non può unire in join la stessa transazione della funzione originale che ha richiamato la stored procedure estesa.  
  
 In modo analogo a una chiamata da un batch o da una stored procedure, la stored procedure estesa viene eseguita nel contesto dell'account di sicurezza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo aspetto deve essere tenuto presente dal proprietario della stored procedure estesa quando vengono concesse ad altri utenti le autorizzazioni per eseguire la procedura.  
  
  
