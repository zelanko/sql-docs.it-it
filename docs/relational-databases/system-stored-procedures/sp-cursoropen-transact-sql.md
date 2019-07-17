---
title: sp_cursoropen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5127d041817a41dcf2d6fb4ed65070c87d05dd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108478"
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Apre un cursore. sp_cursoropen definisce l'istruzione SQL associata al cursore e le opzioni del cursore e quindi popola il cursore. sp_cursoropen equivale alla combinazione del [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni DECLARE_CURSOR e OPEN. Questa routine viene richiamata specificando ID = 2 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 Identificatore del cursore generato da SQL Server. *cursore* è un *gestire* valore che deve essere fornito su tutte le routine successive che riguardano il cursore, ad esempio sp_cursorfetch. *cursore* è un parametro obbligatorio con un **int** valore restituito.  
  
 *cursore* consente a più cursori di essere attivi in un'unica connessione di database.  
  
 *stmt*  
 Parametro obbligatorio che definisce il set di risultati del cursore. Qualsiasi stringa di query valida (sintassi e associazione) di qualsiasi tipo di stringa (indipendentemente da Unicode, dimensione e così via) può essere utilizzato come un valore valido *stmt* tipo valore.  
  
 *scrollopt*  
 Opzione di scorrimento. *scrollopt* è un parametro facoltativo che richiede uno dei seguenti **int** valori di input.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 A causa della possibilità che il valore richiesto non è appropriato per il cursore definito da *stmt*, questo parametro funge sia da input e output. In questi casi, SQL Server assegna un valore appropriato.  
  
 *ccopt*  
 Opzioni del controllo della concorrenza. *ccopt* è un parametro facoltativo che richiede uno dei seguenti **int** valori di input.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (precedentemente noto come LOCKCC)|  
|0x0004|**OTTIMISTICA** (precedentemente noto come OPTCC)|  
|0x0008|OPTIMISTIC (precedentemente noto come OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Come per gli *scrollopt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono eseguire l'override di richiesta *ccopt* valori.  
  
 *rowcount*  
 Numero di righe del buffer di recupero da utilizzare con AUTO_FETCH. Il valore predefinito è 20 righe. *conteggio delle righe* si comporta in modo diverso quando assegnato come valore di input rispetto a un valore restituito.  
  
|Come valore di input|Come valore restituito|  
|--------------------|---------------------|  
|Quando il AUTO_FETCH *scrollopt* viene specificato valore *rowcount* rappresenta il numero di righe da inserire nel buffer di recupero.<br /><br /> Nota: > 0 è un valore valido quando viene specificato AUTO_FETCH, ma in caso contrario, viene ignorato.|Rappresenta il numero di righe nel risultato impostato, tranne quando la *scrollopt* viene specificato il valore AUTO_FETCH.|  
  
-  
  
 *boundparam*  
 Indica l'utilizzo di parametri aggiuntivi. *boundparam* è un parametro facoltativo che deve essere specificato se il *scrollopt* valore PARAMETERIZED_STMT è impostata su ON.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Se non viene generato alcun errore, sp_cursoropen restituisce uno dei valori seguenti.  
  
 0  
 La routine è stata effettuata correttamente.  
  
 0x0001  
 Si verificato un errore durante l'esecuzione (un errore minore, non abbastanza grave da compromettere l'operazione).  
  
 0x0002  
 È in corso un'operazione asincrona.  
  
 0x0002  
 È in corso l'elaborazione di un'operazione FETCH.  
  
 A  
 Questo cursore è stato deallocato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non è disponibile.  
  
 Quando viene generato un errore, è possibile che i valori restituiti siano incoerenti. L'accuratezza non può pertanto essere garantita.  
  
 Quando la *rowcount* parametro viene specificato come valore restituito, si verifica il set di risultati seguente.  
  
 -1  
 Valore restituito se il numero di righe è sconosciuto o non applicabile.  
  
 -n  
 Valore restituito quando un popolamento asincrono è attivo. Rappresenta il numero di righe che sono stati posizionati nell'operazione di recupero del buffer quando le *scrollopt* viene specificato il valore AUTO_FETCH.  
  
 Se RPC è in uso, i valori restituiti sono come segue.  
  
 0  
 La routine è stata eseguita correttamente.  
  
 1  
 La routine non è riuscita.  
  
 2  
 È in corso la generazione asincrona di un cursore keyset.  
  
 16  
 Un cursore di avanzamento rapido è stato chiuso automaticamente.  
  
> [!NOTE]  
>  Se la routine sp_cursoropen viene eseguita correttamente, i parametri restituiti RPC e un set di risultati con informazioni sul formato di colonna TDS (0xa0 e 0xa1 messaggi) vengono inviati. Se non riesce, vengono inviati uno o più messaggi di errore TDS. In entrambi i casi, non verranno restituiti dati di riga e il conteggio del messaggio *done* sarà zero. Se si utilizza una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente a 7.0, vengono restituiti i messaggi 0xa0, 0xa1 (standard per le istruzioni SELECT) insieme ai flussi di token 0xa5 e 0xa4. Se si utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, viene restituito 0x81 (standard per le istruzioni SELECT) insieme ai flussi di token 0xa5 e 0xa4.  
  
## <a name="remarks"></a>Note  
  
## <a name="stmt-parameter"></a>Parametro stmt  
 Se *stmt* specifica l'esecuzione di una stored procedure, i parametri di input possono essere definiti come costanti come parte delle *stmt* stringa o specificata come *boundparam* argomenti. È possibile passare variabili dichiarate come parametri associati in questo modo.  
  
 Il contenuto consentito del *stmt* parametro variano a seconda se il *ccopt* restituito ALLOW_DIRECT valore è stato collegato tramite OR al resto del *ccopt* valori, ad esempio:  
  
-   Se non è specificato ALLOW_DIRECT, ovvero un [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT o EXECUTE istruzione chiama una stored procedure contenente una singola istruzione SELECT deve essere utilizzata. Inoltre, l'istruzione SELECT deve essere qualificata come cursore; vale a dire, non può contenere le parole chiave SELECT INTO o FOR BROWSE.  
  
-   Se viene specificato ALLOW_DIRECT, è possibile che vengano eseguite una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)], incluse quelle che, a loro volta, eseguono altre stored procedure con più istruzioni. Le istruzioni non SELECT o qualsiasi istruzione SELECT che contenga le parole chiave SELECT INTO o FOR BROWSE verranno semplicemente eseguite e non comporteranno la creazione di un cursore. Questo vale per qualsiasi istruzione SELECT inclusa in un batch di più istruzioni. Nei casi in cui un'istruzione SELECT contiene clausole che riguardano solo i cursori, tali clausole vengono ignorate. Ad esempio, quando il valore di *ccopt* è 0x2002, si tratta di una richiesta per:  
  
    -   Un cursore con blocchi di scorrimento, se una sola istruzione SELECT è qualificata come cursore oppure  
  
    -   Un'esecuzione diretta di istruzioni in caso di presenza di più istruzioni, di una sola istruzione non SELECT o di un'istruzione SELECT non qualificata come cursore.  
  
## <a name="scrollopt-parameter"></a>Parametro scrollopt  
 I primi cinque *scrollopt* valori (KEYSEY, DYNAMIC, FORWARD_ONLY, STATIC e FAST_FORWARD) si escludono a vicenda.  
  
 PARAMETERIZED_STMT e CHECK_ACCEPTED_TYPES possono essere collegati tramite OR a uno dei primi cinque valori.  
  
 AUTO_FETCH e AUTO_CLOSE possono essere collegati tramite OR a FAST_FORWARD.  
  
 Se CHECK_ACCEPTED_TYPES è ON, almeno uno degli ultimi cinque *scrollopt* valori (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE, FORWARD_ONLY_ACCEPTABLE, STATIC_ACCEPTABLE o FAST_FORWARD_ACCEPTABLE) deve inoltre essere impostata su ON.  
  
 I cursori STATIC sono sempre aperti come READ_ONLY. Ciò significa che non è possibile aggiornare la tabella sottostante tramite questo cursore.  
  
## <a name="ccopt-parameter"></a>Parametro ccopt  
 I primi quattro *ccopt* valori (READ_ONLY, SCROLL_LOCKS ed entrambi i valori OPTIMISTIC) si escludono a vicenda.  
  
> [!NOTE]  
>  Scelta di uno dei primi quattro *ccopt* valori determina se il cursore è di sola lettura, o se vengono utilizzati metodi di blocchi o ottimistici per impedire la perdita di aggiornamenti. Se un *ccopt* valore non è specificato, il valore predefinito è OPTIMISTIC.  
  
 ALLOW_DIRECT e CHECK_ACCEPTED_TYPES possono essere collegati tramite OR a uno dei primi quattro valori.  
  
 UPDT_IN_PLACE può essere collegato tramite OR a READ_ONLY, SCROLL_LOCKS o a uno dei valori OPTIMISTIC.  
  
 Se CHECK_ACCEPTED_TYPES è ON, almeno uno degli ultimi quattro *ccopt* valori (READ_ONLY_ACCEPTABLE, SCROLL_LOCKS_ACCEPTABLE e uno dei valori OPTIMISTIC_ACCEPTABLE) devono inoltre essere ON.  
  
 Funzioni UPDATE e DELETE posizionate possono essere eseguite solo entro il buffer di recupero e solo se il *ccopt* valore è uguale a SCROLL_LOCKS o OPTIMISTIC. Se SCROLL_LOCKS è il valore specificato, la riuscita dell'operazione è garantita. Se OPTIMISTIC è il valore specificato, l'operazione non riuscirà se la riga è stata modificata successivamente all'ultimo recupero.  
  
 Il motivo di questo errore è che, quando il valore specificato è OPTIMISTIC, viene eseguita una funzione di controllo della concorrenza ottimistica mediante il confronto di timestamp o valori di checksum, come determinato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se una delle righe non corrisponde, l'operazione non riesce.  
  
 Specificando UPDT_IN_PLACE come valore restituito, si ottengono i risultati seguenti:  
  
-   Se non viene impostato durante l'esecuzione di un aggiornamento posizionato in una tabella con un indice univoco, il cursore elimina la riga dalla rispettiva tabella di lavoro e la inserisce alla fine di una delle colonne chiave utilizzate dal cursore, modificando in questo modo le colonne.  
  
-   Se impostato su ON, il cursore semplicemente aggiornerà le colonne chiave nella riga originale della tabella di lavoro.  
  
## <a name="boundparam-parameter"></a>Parametro bound_param  
 Il nome del parametro deve essere *paramdef* quando viene specificato PARAMETERIZED_STMT, in base al messaggio di errore nel codice. Quando non è specificato PARAMETERIZED_STMT, nel messaggio di errore non è specificato alcun nome.  
  
## <a name="rpc-considerations"></a>Considerazioni su RPC  
 Per richiedere che vengano restituiti metadati sull'elenco di selezione del cursore nel flusso TDS, è possibile impostare il flag di input RPC RETURN_METADATA su 0x0001.  
  
## <a name="examples"></a>Esempi  
  
### <a name="boundparam-parameter"></a>Parametro bound_param  
 I parametri dopo il quinto vengono passati insieme sul piano dell'istruzione come parametri di input. Il primo parametro di questo tipo deve essere una stringa nel formato:  
  
 *{nome della variabile locale data type} [,... n]*  
  
 I parametri successivi vengono utilizzati per passare i valori con cui sostituire il *nome della variabile locale* nell'istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
