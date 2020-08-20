---
description: Funzioni deterministiche e non deterministiche
title: Funzioni deterministiche e non deterministiche | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2665ab9b5a30209a123056664921334ce3c8367
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485306"
---
# <a name="deterministic-and-nondeterministic-functions"></a>Funzioni deterministiche e non deterministiche
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Le funzioni deterministiche restituiscono sempre lo stesso risultato quando vengono chiamate con un set di valori di input specifico e se lo stato del database rimane invariato. Le funzioni non deterministiche possono restituire risultati diversi quando vengono chiamate con un set di valori di input specifico, anche se lo stato del database a cui accedono rimane invariato. Ad esempio, tramite la funzione AVG viene restituito sempre lo stesso risultato in base alle condizioni indicate in precedenza, ma tramite la funzione GETDATE, mediante la quale viene restituito il valore datetime corrente, viene sempre restituito un risultato diverso.  
  
 Le funzioni definite dall'utente includono diverse proprietà che influiscono sulla capacità del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] di indicizzare i risultati della funzione, tramite gli indici nelle colonne calcolate che chiamano la funzione o tramite le viste indicizzate che fanno riferimento alla funzione. Una di queste proprietà è la proprietà deterministica di una funzione. Non è, ad esempio, possibile creare un indice cluster in una vista se la vista fa riferimento a funzioni non deterministiche. Per altre informazioni sulle proprietà delle funzioni, inclusa la proprietà deterministica, vedere [Funzioni definite dall'utente](../../relational-databases/user-defined-functions/user-defined-functions.md).  
  
 In questo argomento vengono illustrati la proprietà deterministica delle funzioni di sistema predefinite e l'effetto sulla proprietà deterministica delle funzioni definite dall'utente quando contiene una chiamata a stored procedure estese.  
  
## <a name="built-in-function-determinism"></a>Proprietà deterministica delle funzioni predefinite  
 Non è possibile influenzare la proprietà deterministica di alcuna funzione predefinita. Ogni funzione predefinita è deterministica o non deterministica in base al modo in cui viene implementata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, la specifica di una clausola ORDER BY in una query non comporta la modifica del determinismo di una funzione usata nella query in questione.  
  
 Tutte le funzioni per i valori stringa predefinite sono deterministiche, ad eccezione di [FORMAT](../../t-sql/functions/format-transact-sql.md). Per un elenco di queste funzioni, vedere [Funzioni per i valori stringa &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md).  
  
 Le funzioni riportate di seguito, appartenenti alle categorie di funzioni predefinite diverse da quelle per i valori stringa, sono sempre deterministiche.  
  
:::row:::
    :::column:::
        ABS
    :::column-end:::
    :::column:::
        DATEDIFF
    :::column-end:::
    :::column:::
        POWER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ACOS
    :::column-end:::
    :::column:::
        DAY
    :::column-end:::
    :::column:::
        RADIANS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ASIN
    :::column-end:::
    :::column:::
        DEGREES
    :::column-end:::
    :::column:::
        ROUND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATAN
    :::column-end:::
    :::column:::
        EXP
    :::column-end:::
    :::column:::
        SIGN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ATN2
    :::column-end:::
    :::column:::
        FLOOR
    :::column-end:::
    :::column:::
        SIN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CEILING
    :::column-end:::
    :::column:::
        ISNULL
    :::column-end:::
    :::column:::
        SQUARE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COALESCE
    :::column-end:::
    :::column:::
        ISNUMERIC
    :::column-end:::
    :::column:::
        SQRT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COS
    :::column-end:::
    :::column:::
        LOG
    :::column-end:::
    :::column:::
        TAN
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        COT
    :::column-end:::
    :::column:::
        LOG10
    :::column-end:::
    :::column:::
        YEAR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATALENGTH
    :::column-end:::
    :::column:::
        MONTH
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DATEADD
    :::column-end:::
    :::column:::
        NULLIF
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
 Le funzioni elencate di seguito non sono sempre deterministiche, ma possono essere utilizzate in viste indicizzate o indici in colonne calcolate quando vengono specificate in modo deterministico.  
  
|Funzione|Commenti|  
|--------------|--------------|  
|Tutte le funzioni di aggregazione|Tutte le funzioni di aggregazione sono deterministiche a meno che non vengano specificate con le clausole OVER e ORDER BY. Per un elenco di queste funzioni, vedere [Funzioni di aggregazione &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md).|  
|CAST|Deterministica a meno che non sia usata con **datetime**, **smalldatetime**o **sql_variant**.|  
|CONVERT|Deterministica a meno che non si verifichi una delle condizioni seguenti:<br /><br /> <br /><br /> Il tipo di origine è **sql_variant**.<br /><br /> Il tipo di destinazione è **sql_variant** e il relativo tipo di origine è non deterministico.<br /><br /> Il tipo di origine o di destinazione è **datetime** o **smalldatetime**, l'altro tipo di origine o di destinazione è una stringa di caratteri ed è specificato uno stile non deterministico. Per essere deterministico, il parametro di stile deve essere una costante. Gli stili minori o uguali a 100 sono non deterministici, ad eccezione degli stili 20 e 21. Gli stili maggiori di 100 sono deterministici, ad eccezione degli stili 106, 107, 109 e 113.|  
|CHECKSUM|Deterministica, ad eccezione di CHECKSUM(*).|  
|ISDATE|Deterministica solo se utilizzata con la funzione CONVERT, se è specificato il parametro di stile CONVERT e se lo stile non equivale a 0, 100, 9 o 109.|  
|RAND|RAND risulta deterministica solo quando si specifica un parametro per il *valore di inizializzazione* .|  
  
 Tutte le funzioni statistiche di sistema, di configurazione, per i cursori, per i metadati e di sicurezza sono di tipo non deterministico. Per un elenco di queste funzioni, vedere [Funzioni di configurazione &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md), [Funzioni per i cursori &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md), [Funzioni per i metadati &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md), [Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md) e [Funzioni statistiche di sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md).  
  
 Di seguito sono elencate le funzioni predefinite di altre categorie che sono sempre non deterministiche.  
  
:::row:::
    :::column:::
        @@CONNECTIONS
    :::column-end:::
    :::column:::
        GETDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@CPU_BUSY
    :::column-end:::
    :::column:::
        GETUTCDATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@DBTS
    :::column-end:::
    :::column:::
        GET_TRANSMISSION_STATUS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IDLE
    :::column-end:::
    :::column:::
        LAG
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@IO_BUSY
    :::column-end:::
    :::column:::
        LAST_VALUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@MAX_CONNECTIONS
    :::column-end:::
    :::column:::
        LEAD
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_RECEIVED
    :::column-end:::
    :::column:::
        MIN_ACTIVE_ROWVERSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACK_SENT
    :::column-end:::
    :::column:::
        NEWID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@PACKET_ERRORS
    :::column-end:::
    :::column:::
        NEWSEQUENTIALID
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TIMETICKS
    :::column-end:::
    :::column:::
        NEXT VALUE FOR
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_ERRORS
    :::column-end:::
    :::column:::
        NTILE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_READ
    :::column-end:::
    :::column:::
        PARSENAME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        @@TOTAL_WRITE
    :::column-end:::
    :::column:::
        PERCENTILE_CONT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        AT TIME ZONE
    :::column-end:::
    :::column:::
        PERCENTILE_DISC
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CUME_DIST
    :::column-end:::
    :::column:::
        PERCENT_RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CURRENT_TIMESTAMP
    :::column-end:::
    :::column:::
        RAND
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        DENSE_RANK
    :::column-end:::
    :::column:::
        RANK
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        FIRST_VALUE
    :::column-end:::
    :::column:::
        ROW_NUMBER
    :::column-end:::
:::row-end:::   
:::row:::
    :::column:::
        FORMAT
    :::column-end:::
    :::column:::
        TEXTPTR
    :::column-end:::
:::row-end:::
 
## <a name="calling-extended-stored-procedures-from-functions"></a>Chiamata di stored procedure estese da funzioni  
 Le funzioni che chiamano stored procedure estese sono non deterministiche, in quanto le stored procedure estese possono avere effetti collaterali sul database, ovvero possono comportare modifiche di uno stato globale del database, quale un aggiornamento di una tabella o di una risorsa esterna, come un file o la rete, tramite, ad esempio, la modifica di un file o l'invio di un messaggio di posta elettronica. Quando si esegue una stored procedure estesa da una funzione definita dall'utente, il set di risultati restituito potrebbe non essere coerente. Le funzioni definite dall'utente che creano effetti collaterali sul database non sono consigliate.  
  
 Quando viene chiamata dall'interno di una funzione, una stored procedure estesa non può restituire set di risultati al client. Qualsiasi API ODS che restituisca set di risultati al client è in possesso di un codice FAIL.  
  
 La stored procedure estesa può connettersi nuovamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tuttavia, la procedura non può unire in join la stessa transazione della funzione originale che ha richiamato la stored procedure estesa.  
  
 In modo analogo a una chiamata da un batch o da una stored procedure, la stored procedure estesa viene eseguita nel contesto dell'account di sicurezza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le autorizzazioni di questo contesto di protezione devono essere tenute presenti dal proprietario della stored procedure estesa quando vengono concesse ad altri utenti le autorizzazioni per eseguire la procedura.  
  
  
