---
title: sp_cursorfetch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4635bffa5b5b681d0ff202c4231c4d8b8d10ae26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108516"
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera un buffer di una o più righe dal database. Il gruppo di righe di questo buffer viene denominato il cursore *buffer di recupero*. è possibile richiamare sp_cursorfetch specificando ID = 7 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 È un *gestiscono* valore generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e restituito da sp_cursoropen. *cursore* è un parametro obbligatorio che richiede un **int** valore di input. Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 *fetchtype*  
 Specifica il buffer del cursore da recuperare. *fetchType* è un parametro facoltativo che richiede uno dei valori di input interi seguenti.  
  
|Value|NOME|Descrizione|  
|-----------|----------|-----------------|  
|0x0001|FIRST|Recupera il buffer del primo *nrows* righe. Se *nrows* è uguale a 0, il cursore viene posizionato prima del set di risultati e viene restituita alcuna riga.|  
|0x0002|NEXT|Recupera il successivo buffer del *nrows* righe.|  
|0x0004|PREV|Recupera il buffer precedente di *nrows* righe.<br /><br /> Nota: Se si utilizza PREV per un cursore FORWARD_ONLY restituisce un messaggio di errore in quanto FORWARD_ONLY supporta lo scorrimento in una sola direzione.|  
|0x0008|LAST|Recupera l'ultimo buffer di *nrows* righe. Se *nrows* è uguale a 0, il cursore viene posizionato dopo il set di risultati e viene restituita alcuna riga.<br /><br /> Nota: Utilizza LAST per un cursore FORWARD_ONLY, viene restituito un messaggio di errore quanto FORWARD_ONLY supporta lo scorrimento in una sola direzione.|  
|0x10|ABSOLUTE|Recupera un buffer di *nrows* righe inizia con la *rownum* riga.<br /><br /> Nota: Utilizza ABSOLUTE per un cursore DYNAMIC o un cursore FORWARD_ONLY, viene restituito un messaggio di errore in quanto FORWARD_ONLY supporta lo scorrimento in una sola direzione.|  
|0x20|RELATIVE|Recupera il buffer di *nrows* righe inizia con la riga che viene specificata come in corso la *rownum* valore delle righe della prima riga nel blocco corrente. In questo caso *rownum* può essere un numero negativo.<br /><br /> Nota: Se si utilizza RELATIVE per un cursore FORWARD_ONLY restituisce un messaggio di errore in quanto FORWARD_ONLY supporta lo scorrimento in una sola direzione.|  
|0x80|REFRESH|Reinserisce nel buffer dati delle tabelle sottostanti.|  
|0x100|INFO|Recupera informazioni sul cursore. Queste informazioni vengono restituite usando il *rownum* e *nrows* parametri. Pertanto, quando viene specificato INFO, *rownum* e *nrows* diventano parametri di output.|  
|0x200|PREV_NOADJUST|Viene utilizzato come PREV. Se tuttavia l'inizio del set di risultati viene raggiunto prima del previsto, i risultati potrebbero variare.|  
|0x400|SKIP_UPDT_CNCY|Deve essere utilizzato con uno degli altri *fetchtype* valori, ad eccezione di INFO.|  
  
> [!NOTE]  
>  Il valore 0x40 non è supportato.  
  
 Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 *rownum*  
 È un parametro facoltativo che consente di specificare la posizione della riga per ABSOLUTE e INFO *fetchtype* valori usando solo valori interi per input, output o entrambi. *rowNum* funge da offset di riga per il *fetchtype* valore relativo di bit. *rowNum* viene ignorato per tutti gli altri valori. Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
 *nrows*  
 Parametro facoltativo utilizzato per specificare il numero di righe da recuperare. Se *nrows* viene omesso, il valore predefinito è 20 righe. Per impostare la posizione senza restituire dati, specificare un valore pari a 0. Quando *nrows* viene applicato per il *fetchtype* query INFO, restituisce il numero totale di righe nella query in questione.  
  
> [!NOTE]  
>  *nrows* viene ignorato per l'aggiornamento *fetchtype* valore di bit.  
>   
>  Per ulteriori informazioni, vedere la sezione Osservazioni di seguito in questo argomento.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nelle tabelle seguenti vengono indicati i valori che possono essere restituiti quando si specifica il valore di bit INFO.  
  
> [!NOTE]  
>  :   Se viene restituita alcuna riga, il contenuto del buffer rimane inalterato.  
  
|*\<rowNum >*|Impostare su|  
|------------------|------------|  
|Se non aperto|0|  
|Se posizionato prima del set di risultati|0|  
|Se posizionato dopo il set di risultati|-1|  
|Per i cursori STATIC e KEYSET|Numero di riga assoluto della posizione corrente nel set di risultati|  
|Peri cursori DYNAMIC|1|  
|Per ABSOLUTE|-1 restituisce l'ultima riga di un set.<br /><br /> -2 restituisce la penultima riga di un set e così via.<br /><br /> Nota: Se più di una riga è richiesto il recupero in questo caso, le ultime due righe del set di risultati vengono restituite.|  
  
|*\<nrows>*|Impostare su|  
|-----------------|------------|  
|Se non aperto|0|  
|Per i cursori STATIC e KEYSET|In genere la dimensione del keyset corrente.<br /><br /> **-m** se il cursore si trova nella creazione asincrona con *m* righe trovato a questo punto.|  
|Peri cursori DYNAMIC|-1|  
  
## <a name="remarks"></a>Note  
  
## <a name="cursor-parameter"></a>Parametro cursor  
 Prima dell'esecuzione di qualsiasi operazione di recupero, il cursore precede per impostazione predefinita la prima riga del set di risultati.  
  
## <a name="fetchtype-parameter"></a>Parametro fetchtype  
 Ad eccezione di SKIP_UPD_CNCY, i *fetchtype* valori si escludono a vicenda.  
  
 Quando viene specificato SKIP_UPDT_CNCY, i valori della colonna timestamp non vengono scritti nella tabella di keyset quando viene recuperata o aggiornata una riga. Se la riga di keyset viene aggiornata, i valori delle colonne timestamp rimangono inalterati. Se la riga di keyset viene inserita, i valori per le colonne timestamp non sono definiti.  
  
 Per i cursori KEYSET, ciò significa che per la tabella di keyset i valori vengono impostati durante l'ultima operazione FETCH non ignorata, se ne è stata eseguita una. In caso contrario, i valori vengono impostati durante il popolamento.  
  
 Per i cursori DYNAMIC, ciò significa che se l'operazione FETCH viene eseguita con l'aggiornamento, vengono prodotti gli stessi risultati di KEYSET. Per qualsiasi altro tipo di recupero, la tabella di keyset viene troncata. Ciò significa che è in corso l'inserimento delle righe e i valori delle colonne timestamp non vengono definiti. Pertanto, quando si esegue sp_cursorfetch per i cursori DYNAMIC, evitare di utilizzare SKIP_UPDT_CNCY per qualsiasi operazione diversa da REFRESH.  
  
 Se un'operazione di recupero non riesce perché la posizione del cursore richiesta è oltre il set di risultati, la posizione del cursore viene impostata subito dopo l'ultima riga. Se un'operazione di recupero non riesce perché la posizione del cursore richiesta è prima del set di risultati, la posizione del cursore viene impostata prima della prima riga.  
  
## <a name="rownum-parameter"></a>Parametro rownum  
 Quando si usa *rownum*, viene riempito il buffer inizia con la riga specificata.  
  
 Il *fetchtype* assoluto fa riferimento alla posizione del valore *rownum* all'interno i risultati completi impostare. Un numero negativo per ABSOLUTE specifica che l'operazione inizia a contare le righe a partire dalla fine del set di risultati.  
  
 Il *fetchtype* relativo fa riferimento alla posizione del valore *rownum* rispetto alla posizione del cursore all'inizio del buffer corrente. Un numero negativo per RELATIVE specifica che il cursore va all'indietro a partire dalla posizione corrente.  
  
## <a name="nrows-parameter"></a>Parametro nrows  
 Il *fetchtype* valori REFRESH e INFO ignorano questo parametro.  
  
 Quando si specifica un *fetchtype* valore del primo con un *nrow* pari a 0, il cursore sono posizionato prima del set di risultati che non è presenti righe nel buffer di recupero.  
  
 Quando si specifica un *fetchtype* valore dell'ultimo con un *nrow* pari a 0, il cursore viene posizionato dopo il set di risultati che non è presenti righe nel buffer di recupero corrente.  
  
 Per il *fetchtype* i valori del successivo, PREV, ABSOLUTE, RELATIVE e PREV_NOADJUST, un *nrow* valore pari a 0 non è valido.  
  
## <a name="rpc-considerations"></a>Considerazioni su RPC  
 Lo stato restituito di RPC indica se il parametro di dimensione del keyset è finale oppure no, cioè se è in corso il popolamento asincrono nel keyset o nella tabella temporanea.  
  
 Il parametro di stato di RPC viene impostato su uno dei valori mostrati nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|La routine è stata eseguita correttamente.|  
|0x0001|La routine non è riuscita.|  
|0x0002|Un recupero in direzione negativa ha impostato la posizione del cursore all'inizio del set di risultati, laddove logicamente il recupero avrebbe dovuto trovarsi prima dei risultati.|  
|0x10|Un cursore di avanzamento è stato chiuso automaticamente.|  
  
 Le righe vengono restituite come set tipico di risultati, ovvero il formato della colonna (0x2a), le righe (0xd1), infine done (0xfd). I token di metadati vengono inviati nello stesso formato specificato per sp_cursoropen, vale a dire: 0x81, 0xa5 e 0xa4 per gli utenti di SQL Server 7.0 e così via. Gli indicatori di stato delle righe vengono inviati come colonne nascoste, analogamente alla modalità BROWSE, alla fine di ogni riga con nome di colonna rowstat e tipo di dati INT4. La colonna rowstat può avere uno dei valori mostrati nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 Poiché il protocollo TDS non consente di inviare la colonna dello stato finale senza inviare le colonne precedenti, per le righe mancanti vengono inviati dati fittizi, cioè campi che ammettono i valori Null, campi a lunghezza fissa impostati su 0, vuoti oppure il valore predefinito per quella colonna, a seconda della situazione specifica.  
  
 Il conteggio delle righe per DONE sarà sempre zero. Il messaggio DONE include il conteggio delle righe del set di risultati effettivo. Tra i messaggi TDS potrebbero essere visualizzati messaggi di errore o informativi.  
  
 Per richiedere che vengano restituiti metadati sull'elenco di selezione del cursore nel flusso TDS, impostare il flag di input RPC RETURN_METADATA su 1.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>R. Utilizzo di PREV per modificare una posizione del cursore  
 Si supponga che un cursore h2 produca un set di risultati con il contenuto seguente con la posizione corrente mostrata di seguito:  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 Successivamente, un'operazione PREV sp_cursorfetch con un *nrows* valore pari a 5 posizioni logicamente il cursore due righe prima della prima riga del set di risultati. In questi casi, il cursore viene regolato in modo da partire dalla prima riga e restituire il numero di righe richieste. Questo spesso significa che restituirà righe che si trovavano nel buffer di recupero di PRIOR.  
  
> [!NOTE]  
>  Si tratta esattamente del caso in cui il parametro di stato di RPC è impostato su 2.  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. Utilizzo di PREV_NOADJUST per restituire un numero inferiore di righe rispetto a PREV  
 PREV_NOADJUST non include mai nel blocco di righe che restituisce le righe che si trovano in corrispondenza della posizione corrente del cursore o dopo tale posizione. Nei casi in cui PREV restituisce righe dopo la posizione corrente, PREV_NOADJUST restituisce meno righe rispetto a quanto richiesto *nrows*. Dato il corrente posizionare nell'esempio A precedente, quando viene applicato PREV, sp_cursorfetch (h2, 4, 1, 5) recupera le righe seguenti:  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 Tuttavia, quando viene applicato PREV_NOADJUST, sp_cursorfetch (h2, 512, 6, 5) recupera solo le righe seguenti:  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
