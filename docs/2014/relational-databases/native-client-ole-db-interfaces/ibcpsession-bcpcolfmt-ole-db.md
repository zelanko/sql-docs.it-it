---
title: IBCPSession::BCPColFmt (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPColFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColFmt method
ms.assetid: 2852f4ba-f1c6-4c4c-86b2-b77e4abe70de
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e896f3e04d24becf136b7abefcff9dbe97fa0970
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63240268"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
  Crea un'associazione tra variabili di programma e colonne di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT BCPColFmt(   
DBORDINALidxUserDataCol,  
inteUserDataType,  
intcbIndicator,  
intcbUserData,  
BYTE *pbUserDataTerm,  
intcbUserDataTerm,  
DBORDINALidxServerCol);  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **BCPColFmt** viene usato per creare un'associazione tra i campi del file di dati BCP e le colonne di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Accetta come parametri la lunghezza, il tipo, il carattere di terminazione e la lunghezza del prefisso di una colonna e imposta ciascuna di queste proprietà per i singoli campi.  
  
 Se l'utente sceglie la modalità interattiva, questo metodo viene chiamato due volte, una volta per impostare il formato della colonna in base ai valori predefiniti (che dipendono dal tipo di colonna del server) e una volta per impostare il formato in base al tipo di client selezionato durante la modalità interattiva, per ogni colonna.  
  
 Nelle modalità non interattive, viene chiamato una sola volta per colonna per impostare il tipo di ogni colonna sul carattere o sul tipo nativo e impostare i caratteri di terminazione di colonna e riga.  
  
 Il metodo **BCPColFmt** consente di specificare il formato del file utente per le copie bulk. Per la copia bulk, un formato contiene le parti seguenti:  
  
-   Un mapping dai campi del file utente alle colonne del database.  
  
-   Il tipo di dati di ogni campo del file utente.  
  
-   La lunghezza dell'indicatore facoltativo per ogni campo.  
  
-   La lunghezza massima dei dati per ogni campo del file utente.  
  
-   La sequenza di byte di terminazione facoltativa per ogni campo.  
  
-   La lunghezza della sequenza di byte di terminazione facoltativa.  
  
 Ogni chiamata a **BCPColFmt** specifica il formato per un campo del file utente. Per modificare ad esempio le impostazioni predefinite per tre campi in un file di dati dell'utente con cinque campi, chiamare prima `BCPColumns(5)` e quindi chiamare **BCPColFmt** cinque volte, con tre di queste chiamate che impostano il formato personalizzato. Per le due chiamate rimanenti, impostare *eUserDataType* su BCP_TYPE_DEFAULT e *cbIndicator*, *cbUserData* e *cbUserDataTerm* su 0, BCP_VARIABLE_LENGTH e 0 rispettivamente. Questa procedura consente di copiare tutte e cinque le colonne, tre con il formato personalizzato e due con il formato predefinito.  
  
> [!NOTE]  
>  Il metodo [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) deve essere chiamato prima di qualsiasi chiamata a **BCPColFmt**. È necessario chiamare **BCPColFmt** una volta per ogni colonna del file utente. Se **BCPColFmt** viene chiamato più di una volta per qualsiasi colonna del file utente, viene generato un errore.  
  
 Non è necessario copiare tutti i dati di un file utente in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ignorare una colonna, specificare il formato dei dati per la colonna impostando il parametro idxServerCol su 0. Per ignorare un campo, è necessario comunque disporre di tutte le informazioni affinché il metodo possa funzionare correttamente.  
  
 **Nota** La funzione [IBCPSession::BCPWriteFmt](ibcpsession-bcpwritefmt-ole-db.md) può essere usata per rendere persistente la specifica del formato fornita tramite **BCPColFmt**.  
  
## <a name="arguments"></a>Argomenti  
 *idxUserDataCol*[in]  
 Indice del campo nel file di dati dell'utente.  
  
 *eUserDataType*[in]  
 Il tipo di dati del campo nel file di dati dell'utente. I tipi di dati disponibili sono elencati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di intestazione di Native Client (sqlncli. h) con BCP_TYPE_XXX formato, ad esempio BCP_TYPE_SQLINT4. Se viene specificato il valore BCP_TYPE_DEFAULT, il provider tenta di utilizzare lo stesso tipo della colonna della tabella o della vista. Per le operazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copia bulk in un file quando l' `eUserDataType` argomento è BCP_TYPE_SQLDECIMAL o BCP_TYPE_SQLNUMERIC:  
  
-   Se la colonna di origine non è decimal o numeric, vengono utilizzate la precisione e la scala predefinite.  
  
-   Se la colonna di origine è decimal o numeric, vengono utilizzate la precisione e la scala della colonna di origine.  
  
 *cbIndicator*[in]  
 Lunghezza del prefisso per il campo. Il prefisso predefinito è BCP_PREFIX_DEFAULT. Le lunghezze valide per il prefisso sono 0, 1, 2, 4 e 8. Una dimensione del prefisso pari a 8 in genere viene utilizzata per indicare che il campo è Chunked e consente di eseguire in modo efficace la copia bulk di colonne del tipo valore di grandi dimensioni.  
  
 *cbUserData*[in]  
 Lunghezza massima, espressa in byte, dei dati del campo nel file utente, senza includere la lunghezza di un carattere di terminazione o di un indicatore di lunghezza.  
  
 L' `cbUserData` impostazione di su BCP_LENGTH_NULL indica che tutti i valori nei campi del file di dati sono o devono essere impostati su null. Impostando `cbUserData` su BCP_LENGTH_VARIABLE indica che il sistema deve determinare la lunghezza dei dati per ogni campo. Per alcuni campi, questo potrebbe indicare che viene generato un indicatore di lunghezza o Null da anteporre ai dati in una copia da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o che l'indicatore è previsto nei dati copiati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati character e `cbUserData` binary, può essere BCP_LENGTH_VARIABLE, BCP_LENGTH_NULL, 0 o un valore positivo. Se `cbUserData` è BCP_LENGTH_VARIABLE, il sistema utilizza l'indicatore di lunghezza, se presente, o una sequenza di caratteri di terminazione per determinare la lunghezza dei dati. Se vengono specificati sia un indicatore di lunghezza che una sequenza di caratteri di terminazione, la copia bulk utilizza la modalità che comporta la copia del minor numero di dati. Se `cbUserData` è BCP_LENGTH_VARIABLE, il tipo di dati è [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tipo carattere o binario e se non viene specificato né un indicatore di lunghezza né una sequenza di caratteri di terminazione, il sistema restituisce un messaggio di errore.  
  
 Se `cbUserData` è 0 o un valore positivo, il sistema utilizza `cbUserData` come lunghezza massima dei dati. Tuttavia, se, oltre a un valore positivo `cbUserData`, viene specificato un indicatore di lunghezza o una sequenza di caratteri di terminazione, il sistema determina la lunghezza dei dati utilizzando il metodo che comporta la copia del minor numero di dati.  
  
 Il `cbUserData` valore rappresenta il numero di byte di dati. Se i dati di tipo carattere sono rappresentati da caratteri wide Unicode `cbUserData` , un valore di parametro positivo rappresenta il numero di caratteri moltiplicato per la dimensione, in byte, di ogni carattere.  
  
 *pbUserDataTerm*[size_is][in]  
 Sequenza di caratteri di terminazione da utilizzare per il campo. Questo parametro risulta particolarmente utile per i dati di tipo carattere, in quanto tutti gli altri tipi hanno una lunghezza fissa o, nel caso dei dati binari, richiedono un indicatore di lunghezza per registrare in modo accurato il numero di byte presenti.  
  
 Per evitare di terminare i dati estratti o per indicare che i dati di un file utente non devono essere terminati, impostare questo parametro su NULL.  
  
 Se si utilizzano più modalità per definire la lunghezza delle colonne di un file utente, ad esempio un carattere di terminazione e un indicatore di lunghezza o un carattere di terminazione e una lunghezza di colonna massima, la copia bulk sceglierà quella che comporta la copia del minor numero di dati.  
  
 L'API della copia bulk esegue la conversione dei caratteri da Unicode a MBCS in base alle necessità. Verificare attentamente che la stringa di byte del carattere di terminazione e la lunghezza della stringa di byte siano impostate correttamente.  
  
 *cbUserDataTerm*[in]  
 Lunghezza, espressa in byte, della sequenza di caratteri di terminazione da utilizzare per la colonna. Se non sono presenti caratteri di terminazione nei dati o non si desidera includerli, impostare questo valore su 0.  
  
 *idxServerCol*[in]  
 Posizione ordinale della colonna nella tabella del database. Il numero della prima colonna è 1. La posizione ordinale di una colonna viene indicata da **IColumnsInfo::GetColumnInfo** o da metodi simili. Se questo valore è 0, la copia bulk ignora il campo nel file di dati.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 S_OK  
 Il metodo è riuscito.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. per informazioni dettagliate, utilizzare l'interfaccia [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Non è stato ad esempio chiamato il metodo [IBCPSession::BCPInit](ibcpsession-bcpinit-ole-db.md) prima della chiamata a questo metodo.  
  
 E_INVALIDARG  
 L'argomento non è valido.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
## <a name="see-also"></a>Vedi anche  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Esecuzione di operazioni di copia bulk](../native-client/features/performing-bulk-copy-operations.md)  
  
  
