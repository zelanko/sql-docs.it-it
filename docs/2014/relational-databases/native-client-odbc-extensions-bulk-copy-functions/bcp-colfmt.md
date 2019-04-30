---
title: bcp_colfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c583ffad2267a82c39d4ab6c7cd71a1852c7cb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065459"
---
# <a name="bcpcolfmt"></a>bcp_colfmt
  Specifica il formato di origine o di destinazione dei dati in un file utente. Quando viene utilizzato come formato di origine, **bcp_colfmt** specifica il formato di un file di dati esistente utilizzato come origine dei dati in una copia bulk da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella. Quando usato come formato di destinazione, il file di dati viene creato utilizzando i formati di colonna specificati con **bcp_colfmt**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_colfmt (  
HDBC   
hdbc  
,  
INT  
idxUserDataCol  
,  
BYTE   
eUserDataType  
,  
INT   
cbIndicator  
,  
DBINT   
cbUserData  
,  
LPCBYTE   
pUserDataTerm  
,  
INT   
cbUserDataTerm  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *idxUserDataCol*  
 Numero ordinale di colonna nel file di dati dell'utente per il quale viene specificato il formato. La prima colonna è 1.  
  
 *eUserDataType*  
 Tipo di dati della colonna nel file utente. Se diverso dal tipo di dati della colonna corrispondente nella tabella di database (*idxServerColumn*), la copia bulk converte i dati, se possibile.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ha introdotto il supporto per i token tipo dati SQLXML e SQLUDT nel *eUserDataType* parametro.  
  
 Il *eUserDataType* parametro viene enumerato in base il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] token dei tipi di dati in SQLNCLI. h, i non enumeratori dei tipi di dati C ODBC. È ad esempio possibile specificare una stringa di caratteri SQL_C_CHAR di tipo ODBC utilizzando il tipo SQLCHARACTER specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per specificare la rappresentazione predefinita dei dati per il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], impostare questo parametro su 0.  
  
 Per una copia bulk fuori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file, quando si *eUserDataType* è SQLDECIMAL o SQLNUMERIC:  
  
-   Se la colonna di origine non è **decimale** oppure **numerico**, vengono utilizzate la precisione predefinita e la scala.  
  
-   Se la colonna di origine **decimale** oppure **numerico**, vengono utilizzate la precisione e scala della colonna di origine.  
  
 *cbIndicator*  
 Lunghezza, espressa in byte, di un indicatore di lunghezza o Null nei dati della colonna. Valori di lunghezza di indicatore validi sono 0 (nel caso in cui non venga utilizzato un indicatore), 1, 2, 4 o 8.  
  
 Per specificare l'utilizzo di un indicatore di copia bulk predefinito, impostare questo parametro su SQL_VARLEN_DATA.  
  
 Gli indicatori vengono visualizzati in memoria direttamente prima dei dati e nel file di dati immediatamente prima dei dati a cui si riferiscono.  
  
 Se si utilizzano più modalità per specificare la lunghezza delle colonne del file di dati, ad esempio un indicatore e una lunghezza di colonna massima o un indicatore e una sequenza di caratteri di terminazione, la copia bulk sceglie quella che comporta la copia del minor numero di dati.  
  
 I file di dati generati dalla copia bulk quando il formato dei dati non viene modificato dall'utente contengono indicatori se la lunghezza dei dati di colonna può variare o se la colonna può accettare NULL come valore.  
  
 *cbUserData*  
 Lunghezza massima, espressa in byte, dei dati della colonna nel file utente, senza includere la lunghezza di un carattere di terminazione o di un indicatore di lunghezza.  
  
 L'impostazione *cbUserData* su SQL_NULL_DATA indica che tutti i valori nella colonna del file di dati sono, o deve essere impostato su NULL.  
  
 L'impostazione *cbUserData* su SQL_VARLEN_DATA indica che il sistema deve determinare la lunghezza dei dati in ogni colonna. Per alcune colonne, ciò può indicare che viene generato un indicatore di lunghezza o Null da anteporre ai dati in una copia da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o che l'indicatore è previsto nei dati copiati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caratteri e tipi di dati binari *cbUserData* può essere SQL_VARLEN_DATA, SQL_NULL_DATA, 0 o un valore positivo. Se *cbUserData* è SQL_VARLEN_DATA, il sistema utilizza l'indicatore di lunghezza, se presente, o una sequenza di caratteri di terminazione per determinare la lunghezza dei dati. Se vengono specificati sia un indicatore di lunghezza che una sequenza di caratteri di terminazione, la copia bulk utilizza la modalità che comporta la copia del minor numero di dati. Se *cbUserData* è SQL_VARLEN_DATA, i dati di tipo è un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carattere o binario e né un indicatore di lunghezza né una sequenza di caratteri di terminazione è specificata, il sistema restituisce un messaggio di errore.  
  
 Se *cbUserData* è 0 o un valore positivo, il sistema usa *cbUserData* come lunghezza massima dei dati. Se, tuttavia, oltre a un *cbUserData* positivo, viene specificato un indicatore di lunghezza o una sequenza di caratteri di terminazione, il sistema determina la lunghezza dei dati usando il metodo che comporta la copia della quantità minima di dati.  
  
 Il valore *cbUserData* rappresenta il numero di byte dei dati. Se i dati di tipo carattere sono rappresentati da caratteri wide Unicode, un valore positivo per il parametro *cbUserData* rappresenta il numero di caratteri moltiplicato per la dimensione, espressa in byte, di ogni carattere.  
  
 *pUserDataTerm*  
 Sequenza di caratteri di terminazione da utilizzare per la colonna. Questo parametro risulta particolarmente utile per i dati di tipo carattere, in quanto tutti gli altri tipi hanno una lunghezza fissa o, nel caso dei dati binari, richiedono un indicatore di lunghezza per registrare in modo accurato il numero di byte presenti.  
  
 Per evitare di terminare i dati estratti o per indicare che i dati di un file utente non devono essere terminati, impostare questo parametro su NULL.  
  
 Se si utilizzano più modalità per definire la lunghezza delle colonne di un file utente, ad esempio un carattere di terminazione e un indicatore di lunghezza o un carattere di terminazione e una lunghezza di colonna massima, la copia bulk sceglierà quella che comporta la copia del minor numero di dati.  
  
 L'API della copia bulk esegue la conversione dei caratteri da Unicode a MBCS in base alle necessità. Verificare attentamente che la stringa di byte del carattere di terminazione e la lunghezza della stringa di byte siano impostate correttamente.  
  
 *cbUserDataTerm*  
 Lunghezza, espressa in byte, della sequenza di caratteri di terminazione da utilizzare per la colonna. Se non sono presenti caratteri di terminazione nei dati o non si desidera includerli, impostare questo valore su 0.  
  
 *idxServerCol*  
 Posizione ordinale della colonna nella tabella di database. Il numero della prima colonna è 1. La posizione ordinale di una colonna viene indicata da [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
 Se questo valore è 0, la copia bulk ignora la colonna nel file di dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Il **bcp_colfmt** funzione consente di specificare il formato del file utente per le copie bulk. Per la copia bulk, un formato contiene le parti seguenti:  
  
-   Un mapping dalle colonne del file utente alle colonne del database.  
  
-   Il tipo di dati di ogni colonna del file utente.  
  
-   La lunghezza dell'indicatore facoltativo per ogni colonna.  
  
-   La lunghezza massima dei dati per ogni colonna del file utente.  
  
-   La sequenza di byte di terminazione facoltativa per ogni colonna.  
  
-   La lunghezza della sequenza di byte di terminazione facoltativa.  
  
 Ogni chiamata a **bcp_colfmt** specifica il formato per una colonna del file utente. Ad esempio, per modificare le impostazioni predefinite per tre colonne in un file di dati utente cinque colonne, chiamare innanzitutto [bcp_columns](bcp-columns.md)**(5)**, quindi chiamare **bcp_colfmt** cinque volte, con tre di queste chiamate impostano il formato personalizzato. Per le due chiamate rimanenti, impostare *eUserDataType* su 0 e impostare *cbIndicator*, *cbUserData*, e *cbUserDataTerm* su 0, SQL_VARLEN Data e 0 rispettivamente. Questa procedura consente di copiare tutte e cinque le colonne, tre con il formato personalizzato e due con il formato predefinito.  
  
 Per la *cbIndicator*, un valore pari a 8 per indicare un tipo di valore elevato è ora valido. Se si specifica il prefisso per un campo la cui colonna corrispondente è un nuovo tipo max, può essere impostato solo su 8. Per informazioni dettagliate, vedere [bcp_bind](bcp-bind.md).  
  
 Il **bcp_columns** funzione deve essere chiamata prima delle chiamate a **bcp_colfmt**.  
  
 È necessario chiamare **bcp_colfmt** una volta per ogni colonna nel file utente.  
  
 La chiamata **bcp_colfmt** più di una volta per qualsiasi file utente colonna, viene generato un errore.  
  
 Non è necessario copiare tutti i dati di un file utente nella tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ignorare una colonna, specificare il formato dei dati per la colonna, impostando il *idxServerCol* parametro su 0. Se si desidera ignorare una colonna, è necessario specificarne il tipo.  
  
 Il [bcp_writefmt](bcp-writefmt.md) funzione può essere utilizzata per rendere persistente la specifica di formato.  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>Supporto di bcp_colfmt per le caratteristiche avanzate di data e ora  
 Per informazioni sui tipi utilizzati con il *eUserDataType* parametro per i tipi data/ora, vedere [modifiche apportate alla copia Bulk per avanzate di data e ora tipi &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
