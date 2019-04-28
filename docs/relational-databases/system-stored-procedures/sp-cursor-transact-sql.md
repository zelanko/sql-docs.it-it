---
title: sp_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3277e64e4c4e04e270298d3532ebc0c2b1f93c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724206"
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Richiede aggiornamenti posizionati. Con questa routine è possibile effettuare operazioni in una o più righe all'interno del buffer di recupero di un cursore. richiamare sp_cursor specificando ID = 1 in un pacchetto del flusso TDS.  
  
||  
|-|  
|**Si applica a**: SQL Server ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] attraverso [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 Handle del cursore. *cursore* è un parametro obbligatorio che richiede un **int** valore di input. *cursore* è il *gestire* valore generato da SQL Server e restituito dalla routine sp_cursoropen.  
  
 *optype*  
 Parametro obbligatorio che definisce l'operazione che verrà effettuata dal cursore. *optype* richiede uno dei seguenti **int** valori di input.  
  
|Value|Nome|Descrizione|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|Consente di aggiornare una o più righe nel buffer di recupero.  Le righe specificate *rownum* nuovamente accessibili e aggiornato.|  
|0x0002|DELETE|Consente di eliminare una o più righe nel buffer di recupero. Le righe specificate *rownum* vengono nuovamente accesso ed eliminazione.|  
|0X0004|INSERT|Inserisce dati senza compilare SQL **Inserisci** istruzione.|  
|0X0008|REFRESH|Consente di inserire nuovamente dati nel buffer dalle tabelle sottostanti e può essere usato per aggiornare la riga nel caso in cui un aggiornamento o un'eliminazione non riesca a causa del controllo della concorrenza ottimistica oppure dopo un'operazione UPDATE.|  
|0X10|LOCK|Fa sì che un SQL Server U-acquisizione del blocco nella pagina contenente la riga specificata. Tale blocco è compatibile con i blocchi S ma non con i blocchi X o con altri blocchi U. Può essere usato per implementare la funzione di blocco a breve termine.|  
|0X20|SETPOSITION|Viene usato solo quando il programma sta per rilasciare un successive di SQL Server posizionata l'istruzione DELETE o UPDATE.|  
|0X40|ABSOLUTE|Può essere usato solo insieme ad UPDATE o DELETE.  ABSOLUTE viene usato solo con i cursori KEYSET, viene ignorato per i cursori DYNAMIC e i cursori STATIC non possono essere aggiornati.<br /><br /> Nota: Se ABSOLUTE viene specificato in una riga nel keyset che non sono stati recuperati, l'operazione non riesca il controllo della concorrenza e il risultato restituito non può essere garantito.|  
  
 *rownum*  
 Specifica le righe del buffer di recupero che verranno usate, aggiornate o eliminate mediante il cursore.  
  
> [!NOTE]  
>  Non influisce sul punto di partenza di qualsiasi operazione di recupero RELATIVE, NEXT o PREVIOUS, né su eliminazioni o aggiornamenti eseguiti utilizzando sp_cursor.  
  
 *rowNum* è un parametro obbligatorio che richiede un **int** valore di input.  
  
 1  
 Indica la prima riga del buffer di recupero.  
  
 2  
 Indica la seconda riga del buffer di recupero.  
  
 3, 4, 5  
 Indica la terza riga e così via.  
  
 n  
 Indica l'ennesima riga del buffer di recupero.  
  
 0  
 Indica tutte le righe del buffer di recupero.  
  
> [!NOTE]  
>  È valida solo per uso con UPDATE, DELETE, REFRESH o LOCK *optype* valori.  
  
 *table*  
 Nome della tabella che identifica la tabella che *optype* da applicare quando la definizione di cursore comporta un join o vengono restituiti i nomi di colonna ambiguo per il *valore* parametro. Se non è definita una tabella specifica, l'impostazione predefinita è la prima tabella nella clausola FROM. *tabella* è un parametro facoltativo che richiede un valore di input di stringa. È possibile specificare la stringa come qualsiasi tipo di dati UNICODE o carattere. *tabella* può essere un nome di tabella in più parti.  
  
 *Valore*  
 Usato per inserire o aggiornare valori. Il *valore* stringa parametro viene utilizzato solo con UPDATE e INSERT *optype* valori. È possibile specificare la stringa come qualsiasi tipo di dati UNICODE o carattere.  
  
> [!NOTE]  
>  I nomi di parametro per *valore* possono essere assegnati dall'utente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Quando si usa una chiamata RPC, un'operazione DELETE o UPDATE posizionata con un numero di buffer 0 restituirà un messaggio DONE con un *rowcount* pari a 0 (esito negativo) o 1 (esito positivo) per ogni riga nel buffer di recupero.  
  
## <a name="remarks"></a>Note  
  
## <a name="optype-parameter"></a>Parametro optype  
 Fatta eccezione per le combinazioni di SETPOSITION con UPDATE, DELETE, REFRESH o LOCK; oppure di ABSOLUTE con UPDATE o DELETE, il *optype* valori si escludono a vicenda.  
  
 La clausola SET del valore UPDATE viene costruita dal *valore* parametro.  
  
 Un vantaggio dell'utilizzo di inserimento *optype* valore è possibile evitare di conversione dei dati non carattere in formato carattere per gli inserimenti. I valori vengono specificati con le stesse modalità di UPDATE. Se non sono incluse colonne obbligatorie, l'operazione INSERT non riesce.  
  
-   Il valore SETPOSITION non influisce sul punto di partenza di qualsiasi operazione di recupero RELATIVE, NEXT o PREVIOUS, né su eliminazioni o aggiornamenti eseguiti utilizzando l'interfaccia di sp_cursor. Qualsiasi numero che non specifichi una riga nel buffer di recupero comporterà l'impostazione della posizione su 1 senza restituzione di errori. Dopo l'esecuzione di SETPOSITION, la posizione rimane attiva fino alla successiva operazione sp_cursorfetch, T-SQL **recuperare** o sp_cursor SETPOSITION con lo stesso cursore. Un'operazione sp_cursorfetch successiva imposterà la posizione del cursore sulla prima riga nel nuovo buffer di recupero, mentre le altre chiamate del cursore non influiranno sul valore della posizione. SETPOSITION può essere collegato da una clausola OR con REFRESH, UPDATE, DELETE o LOCK allo scopo di impostare il valore della posizione sull'ultima riga modificata.  
  
 Se una riga nel buffer di recupero non viene specificata tramite il *rownum* parametro, la posizione verrà impostata su 1, senza errori restituiti. Dopo l'impostazione, la posizione rimane effettiva fino a quando non verrà eseguita sullo stesso cursore la successiva operazione sp_cursorfetch, T-SQL o SETPOSITION di sp_cursor.  
  
 SETPOSITION può essere collegato da una clausola OR con REFRESH, UPDATE, DELETE o LOCK allo scopo di impostare la posizione del cursore sull'ultima riga modificata.  
  
## <a name="rownum-parameter"></a>Parametro rownum  
 Se specificato, il *rownum* parametro può essere interpretato come numero di riga all'interno del keyset anziché il numero di riga nel buffer di recupero. È responsabilità dell'utente garantire la gestione del controllo della concorrenza. Ciò significa che per i cursori SCROLL_LOCKS è necessario gestire indipendentemente un blocco nella riga specificata. Questa operazione può essere eseguita tramite una transazione. Per eseguire questa operazione con i cursori OPTIMISTIC, è necessario avere recuperato la riga precedentemente.  
  
## <a name="table-parameter"></a>Parametro table  
 Se il *optype* valore è UPDATE o INSERT e un aggiornamento completo o l'istruzione insert viene inviata come le *valore* parametro, il valore specificato per *tabella* viene ignorato.  
  
> [!NOTE]  
>  È possibile modificare una sola tabella che partecipa a una vista. Il *valore* nomi delle colonne di parametro devono riflettere i nomi di colonna nella vista, ma il nome della tabella può essere quello della tabella di base sottostante (nel qual caso sp_cursor sostituirà il nome della vista).  
  
## <a name="value-parameter"></a>Parametro value  
 Esistono due alternative alle regole per l'utilizzo *valore* come indicato in precedenza nella sezione argomenti:  
  
1.  È possibile usare un nome che è '\@"anteposto al nome della colonna nell'elenco di selezione per qualsiasi denominato *valore* parametri. Un vantaggio di questa alternativa consiste nella possibilità che la conversione di dati non sia necessaria.  
  
2.  Usare un parametro di inviare un'istruzione UPDATE o INSERT completa oppure usare più parametri per inviare parti di un'istruzione UPDATE o INSERT che SQL Server verranno compilate in un'istruzione completa. È possibile trovare alcuni esempi nella sezione Esempi più avanti in questo argomento.  
  
## <a name="examples"></a>Esempi  
  
### <a name="alternative-value-parameter-uses"></a>Utilizzi alternativi del parametro value  
 Per UPDATE:  
  
 Quando viene usato un solo parametro, si potrebbe inviare un'istruzione UPDATE usando la sintassi seguente:  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  Se UPDATE \<nome tabella > è specificato, qualsiasi valore specificato per il *tabella* parametro verrà ignorato.  
  
 Quando vengono usati più parametri, il primo parametro deve essere una stringa nel formato seguente:  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 e i parametri successivi devono essere nel formato:  
  
 `<column name> = expression  [,...n]`  
  
 In questo caso, il \<nome tabella > nell'aggiornamento costruita istruzione è il valore specificato o impostato sul valore predefinito per il *tabella* parametro.  
  
 Per INSERT:  
  
 Quando viene usato un solo parametro, si potrebbe inviare un'istruzione INSERT usando la sintassi seguente:  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  Se inserire  *\<nome tabella >* viene specificato, qualsiasi valore specificato per il *tabella* parametro verrà ignorato.  
  
 Quando vengono usati più parametri, il primo parametro deve essere una stringa nel formato seguente:  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 e i parametri successivi devono essere nel formato:  
  
 `expression [,...n]`  
  
 ad eccezione dei casi in cui è stato specificato VALUES. In questo caso, l'ultima espressione deve essere seguita da una parentesi finale ")". In questo caso, il  *\<nome tabella >* nell'aggiornamento costruita istruzione è il valore specificato o impostato sul valore predefinito per il *tabella* parametro.  
  
> [!NOTE]  
>  È possibile inviare un parametro come parametro denominato, ad esempio "`@VALUES`". In questo caso è possibile non usare altri parametri denominati.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
