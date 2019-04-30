---
title: bcp_setcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_setcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d5d777686bd40fa1b405f20da6173fc2de82640
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226238"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
  Il **bcp_setcolfmt** funzione sostituisce le [bcp_colfmt](bcp-colfmt.md). Nello specificare le regole di confronto di colonna, il **bcp_setcolfmt** necessario utilizzare la funzione. [bcp_setbulkmode](bcp-setbulkmode.md) può essere utilizzato per specificare più di un formato di colonna.  
  
 Questa funzione fornisce un approccio flessibile alla definizione del formato delle colonne in un'operazione di copia bulk. La funzione viene utilizzata per impostare singoli attributi di formato di colonna. Ogni chiamata a **bcp_setcolfmt** imposta un attributo di formato di colonna.  
  
 Il **bcp_setcolfmt** funzione specifica il formato di origine o destinazione dei dati in un file utente. Quando viene utilizzato come formato di origine, **bcp_setcolfmt** specifica il formato di un file di dati esistente utilizzato come origine dei dati in una copia bulk in una tabella dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando usato come formato di destinazione, il file di dati viene creato utilizzando i formati di colonna specificati con **bcp_setcolfmt**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_setcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbValue  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *field*  
 Numero di colonna ordinale per cui viene impostata la proprietà.  
  
 *property*  
 Una delle costanti di proprietà. Le costanti della proprietà sono definite nella tabella seguente.  
  
|Proprietà|Value|Descrizione|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|Tipo di dati della colonna nel file utente. Se differisce dal tipo di dati della colonna corrispondente nella tabella del database, la copia bulk converte i dati, se possibile.<br /><br /> Il parametro BCP_FMT_TYPE viene enumerato in base ai token dei tipi di dati in sqlncli.h e non in base agli enumeratori dei tipi di dati C ODBC. È possibile, ad esempio, specificare una stringa di caratteri SQL_C_CHAR di tipo ODBC utilizzando il tipo SQLCHARACTER specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Per specificare la rappresentazione predefinita dei dati per il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], impostare questo parametro su 0.<br /><br /> Per una copia bulk esterna a SQL Server in un file, quando BCP_FMT_TYPE è SQLDECIMAL o SQLNUMERIC:<br /><br /> -Se la colonna di origine non è **decimale** oppure **numerico**, vengono utilizzate la precisione predefinita e la scala.<br />-Se la colonna di origine è **decimale** oppure **numerico**, vengono utilizzate la precisione e scala della colonna di origine.|  
|BCP_FMT_INDICATOR_LEN|INT|Lunghezza in byte dell'indicatore (prefisso).<br /><br /> Lunghezza, espressa in byte, di un indicatore di lunghezza o Null nei dati della colonna. I valori validi per la lunghezza dell'indicatore sono 0 (quando non si utilizza alcun indicatore), 1, 2 o 4.<br /><br /> Per specificare l'utilizzo di un indicatore di copia bulk predefinito, impostare questo parametro su SQL_VARLEN_DATA.<br /><br /> Gli indicatori vengono visualizzati in memoria direttamente prima dei dati e nel file di dati immediatamente prima dei dati a cui si riferiscono.<br /><br /> Se si utilizzano più modalità per specificare la lunghezza delle colonne del file di dati, ad esempio un indicatore e una lunghezza di colonna massima o un indicatore e una sequenza di caratteri di terminazione, la copia bulk sceglie quella che comporta la copia del minor numero di dati.<br /><br /> I file di dati generati dalla copia bulk quando il formato dei dati non viene modificato dall'utente contengono indicatori se la lunghezza dei dati di colonna può variare o se la colonna può accettare NULL come valore.|  
|BCP_FMT_DATA_LEN|DBINT|Lunghezza in byte dei dati (lunghezza di colonna)<br /><br /> Lunghezza massima, espressa in byte, dei dati della colonna nel file utente, esclusa la lunghezza di eventuali caratteri di terminazione o di indicatori di lunghezza.<br /><br /> L'impostazione di BCP_FMT_DATA_LEN su SQL_NULL_DATA indica che tutti i valori nella colonna del file di dati sono o devono essere impostati su NULL.<br /><br /> L'impostazione di BCP_FMT_DATA_LEN su SQL_VARLEN_DATA indica che il sistema deve determinare la lunghezza dei dati in ogni colonna. Per alcune colonne, ciò può indicare che viene generato un indicatore di lunghezza o Null da anteporre ai dati in una copia da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o che l'indicatore è previsto nei dati copiati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Per i tipi di dati character e binary di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], BCP_FMT_DATA_LEN può essere SQL_VARLEN_DATA, SQL_NULL_DATA, 0 o un valore positivo. Se BCP_FMT_DATA_LEN è SQL_VARLEN_DATA, il sistema utilizza l'indicatore di lunghezza, se disponibile, o una sequenza di caratteri di terminazione per determinare la lunghezza dei dati. Se vengono specificati sia un indicatore di lunghezza che una sequenza di caratteri di terminazione, la copia bulk utilizza la modalità che comporta la copia del minor numero di dati. Se BCP_FMT_DATA_LEN è SQL_VARLEN_DATA, il tipo di dati è un tipo character o binary di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non viene specificato né un indicatore di lunghezza né una sequenza di caratteri di terminazione, il sistema restituisce un messaggio di errore.<br /><br /> Se BCP_FMT_DATA_LEN è 0 o un valore positivo, viene utilizzato come lunghezza massima dei dati. Se, tuttavia, oltre a un valore positivo per BCP_FMT_DATA_LEN viene specificato un indicatore di lunghezza o una sequenza di caratteri di terminazione, il sistema determina la lunghezza dei dati utilizzando il metodo che comporta la copia del minor numero di dati.<br /><br /> Il valore di BCP_FMT_DATA_LEN rappresenta il numero di byte dei dati. Se i dati di tipo carattere vengono rappresentati come caratteri estesi Unicode, un valore positivo per il parametro BCP_FMT_DATA_LEN rappresenta il numero di caratteri moltiplicato per le dimensioni, espresse in byte, di ogni carattere.|  
|BCP_FMT_TERMINATOR|LPCBYTE|Puntatore alla sequenza di caratteri di terminazione (ANSI o Unicode in base alle esigenze) da utilizzare per la colonna. Questo parametro risulta particolarmente utile per i dati di tipo carattere, in quanto tutti gli altri tipi hanno una lunghezza fissa o, nel caso dei dati binari, richiedono un indicatore di lunghezza per registrare in modo accurato il numero di byte presenti.<br /><br /> Per evitare di terminare i dati estratti o per indicare che i dati di un file utente non devono essere terminati, impostare questo parametro su NULL.<br /><br /> Se si utilizzano più modalità per definire la lunghezza delle colonne di un file utente, ad esempio un carattere di terminazione e un indicatore di lunghezza o un carattere di terminazione e una lunghezza di colonna massima, la copia bulk sceglierà quella che comporta la copia del minor numero di dati.<br /><br /> L'API della copia bulk esegue la conversione dei caratteri da Unicode a MBCS in base alle necessità. Verificare attentamente che la stringa di byte del carattere di terminazione e la lunghezza della stringa di byte siano impostate correttamente.|  
|BCP_FMT_SERVER_COL|INT|Posizione ordinale della colonna nel database.|  
|BCP_FMT_COLLATION|LPCSTR|Nome delle regole di confronto.|  
  
 *pValue*  
 È il puntatore al valore da associare al *proprietà*. Consente di impostare singolarmente ogni proprietà di formato di colonna.  
  
 *cbvalue*  
 Lunghezza in byte del buffer delle proprietà.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Questa funzione sostituisce le **bcp_colfmt** (funzione). Tutte le funzionalità del **bcp_colfmt** è disponibile in **bcp_setcolfmt** (funzione). Sono inoltre supportate le regole di confronto delle colonne. È consigliabile impostare gli attributi di formato di colonna seguenti nell'ordine indicato:  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 Il **bcp_setcolfmt** funzione consente di specificare il formato del file utente per le copie bulk. Per la copia bulk, un formato contiene le parti seguenti:  
  
-   Un mapping dalle colonne del file utente alle colonne del database.  
  
-   Il tipo di dati di ogni colonna del file utente.  
  
-   La lunghezza dell'indicatore facoltativo per ogni colonna.  
  
-   La lunghezza massima dei dati per ogni colonna del file utente.  
  
-   La sequenza di byte di terminazione facoltativa per ogni colonna.  
  
-   La lunghezza della sequenza di byte di terminazione facoltativa.  
  
 Ogni chiamata a **bcp_setcolfmt** specifica il formato per una colonna del file utente. Ad esempio, per modificare le impostazioni predefinite per tre colonne in un file di dati utente cinque colonne, chiamare innanzitutto [bcp_columns](bcp-columns.md)**(5)**, quindi chiamare **bcp_setcolfmt** cinque volte, con tre di queste chiamate impostano il formato personalizzato. Per le due chiamate rimanenti, impostare BCP_FMT_TYPE su 0 e bcp_fmt_indicator_length, BCP_FMT_DATA_LEN e *cbValue* su 0, SQL_VARLEN_DATA e 0 rispettivamente. Questa procedura consente di copiare tutte e cinque le colonne, tre con il formato personalizzato e due con il formato predefinito.  
  
 Il **bcp_columns** funzione deve essere chiamata prima di chiamare **bcp_setcolfmt**.  
  
 È necessario chiamare **bcp_setcolfmt** una volta per ogni proprietà di ogni colonna nel file utente.  
  
 Non è necessario copiare tutti i dati di un file utente nella tabella di SQL Server. Per ignorare una colonna, specificarne il formato dei dati impostando il parametro BCP_FMT_SERVER_COL su 0. Se si desidera ignorare una colonna, è necessario specificarne il tipo.  
  
 Il [bcp_writefmt](bcp-writefmt.md) funzione può essere utilizzata per rendere persistente la specifica di formato.  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_setcolfmt per le caratteristiche avanzate di data e ora  
 I tipi utilizzati con la proprietà BCP_FMT_TYPE per i tipi di data/ora sono come specificato nella [modifiche apportate alla copia Bulk per avanzate di data e ora i tipi &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
