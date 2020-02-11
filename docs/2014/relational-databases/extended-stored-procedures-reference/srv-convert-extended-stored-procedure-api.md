---
title: srv_convert (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_convert
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_convert
ms.assetid: 216b4a31-786e-4361-8a33-e5f6e9790f90
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6bc430354ca8ef220caed882f1f8c7942b44d158
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127274"
---
# <a name="srv_convert-extended-stored-procedure-api"></a>srv_convert (API Stored procedure estesa)
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Consente di modificare i dati da un tipo all'altro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_convert (  
SRV_PROC *  
srvproc  
,  
int  
srctype  
,  
void *  
src  
,  
DBINT  
srclen  
,  
int  
desttype  
,  
void *  
dest  
,  
DBINT  
destlen  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client. La struttura contiene tutte le informazioni di controllo utilizzate dall'API Stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client. Se specificato, l'handle *srvproc* viene passato alla funzione di gestione degli errori dell'API Stored procedure estesa quando si verifica un errore.  
  
 *srcType*  
 Indica il tipo a cui appartengono i dati da convertire. Questo parametro può appartenere a qualsiasi tipo di dati dell'API Stored procedure estesa.  
  
 *src*  
 Puntatore ai dati da convertire. Questo parametro può appartenere a qualsiasi tipo di dati dell'API Stored procedure estesa.  
  
 *srclen*  
 Specifica la lunghezza, espressa in byte, dei dati da convertire. Se *srclen* è 0, **srv_convert** inserisce un valore Null nella variabile di destinazione. A meno che non sia 0, questo parametro viene ignorato per i tipi di dati a lunghezza fissa e in tal caso si presuppone che i dati di origine siano NULL. Per i dati appartenenti al tipo SRVCHAR, una lunghezza di -1 indica che la stringa ha una terminazione Null.  
  
 *destType*  
 Indica il tipo di dati in cui convertire l'origine. Questo parametro può appartenere a qualsiasi tipo di dati dell'API Stored procedure estesa.  
  
 *dest*  
 Puntatore alla variabile di destinazione che riceve i dati convertiti. Se questo puntatore è NULL, **srv_convert** chiama il gestore degli errori specificato dall'utente, se disponibile, e restituisce -1.  
  
 Se *desttype* è SRVDECIMAL o SRVNUMERIC, il parametro *dest* deve essere un puntatore a una struttura DBNUMERIC o DBDECIMAL con i campi della precisione e della scala della struttura già impostati sui valori desiderati. È possibile utilizzare DEFAULTPRECISION per specificare una precisione predefinita e DEFAULTSCALE per specificare una scala predefinita.  
  
 *destlen*  
 Specifica la lunghezza, espressa in byte, della variabile di destinazione. Questo parametro viene ignorato per i tipi di dati a lunghezza fissa. Per una variabile di destinazione di tipo SRVCHAR, il valore di *destlen* deve essere la lunghezza totale dello spazio del buffer di destinazione. Una lunghezza di -1 per una variabile di destinazione di tipo SRVCHAR o SRVBINARY indica che lo spazio disponibile è sufficiente. Per una variabile di destinazione di tipo *srvchar*, se la lunghezza è pari a -1 la stringa di caratteri include una terminazione Null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La lunghezza dei dati convertiti, espressa in byte, se la conversione del tipo di dati viene eseguita correttamente. Quando **srv_convert** rileva una richiesta di conversione non supportata, chiama il gestore degli errori specificato dallo sviluppatore, se disponibile, imposta un numero di errore globale e restituisce -1.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **srv_willconvert** determina se una specifica conversione è consentita.  
  
 La conversione in tipi di dati numerici approssimati SRVFLT4 o SRVFLT8 può causare una perdita di precisione. Lo stesso problema può verificarsi durante la conversione da tipi di dati numerici approssimati SRVFLT4 o SRVFLT8 in SRVCHAR o SRVTEXT.  
  
 La conversione in SRVFLT*x*, SRVINT*x*, SRVMONEY, SRVMONEY4, SRVDECIMAL o SRVNUMERIC può causare un overflow se il numero è maggiore del valore massimo della destinazione o un underflow se il numero è minore del valore minimo della destinazione. Se l'overflow si verifica durante la conversione in SRVCHAR o SRVTEXT, il primo carattere del valore risultante contiene un asterisco (*) per indicare l'errore.  
  
 Durante la conversione di SRVCHAR in SRVBINARY, **srv_convert** interpreta SRVCHAR come stringa esadecimale, indipendentemente dalla presenza di uno 0 (zero) iniziale nella stringa. Durante la conversione di SRVBINARY in SRVCHAR, **srv_convert** crea una stringa esadecimale senza uno 0 (zero) iniziale. In tutti gli altri casi, una conversione verso o dal tipo di dati SRVBINARY è una copia di bit diretta.  
  
 In determinati casi, può essere utile convertire un tipo di dati in se stesso. La conversione di SRVCHAR in SRVCHAR con un valore di *destlen* pari a -1, ad esempio, aggiunge un carattere di terminazione Null a una stringa.  
  
 Per una descrizione dei tipi di dati e delle conversioni dei tipi di dati dell'API Stored procedure estesa, vedere [Tipi di dati &#40;API Stored procedure estesa&#41;](data-types-extended-stored-procedure-api.md).  
  
 Di seguito sono riportati i motivi per cui la funzione **srv_convert** potrebbe non riuscire:  
  
-   La conversione richiesta non è disponibile.  
  
-   La conversione ha causato un troncamento, un overflow o una perdita di precisione nella variabile di destinazione.  
  
-   Si è verificato un errore di sintassi durante la conversione di una stringa di caratteri in un tipo di dati numerici.  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_setutype &#40;API stored procedure estesa&#41;](srv-setutype-extended-stored-procedure-api.md)   
 [srv_willconvert &#40;API stored procedure estesa&#41;](srv-willconvert-extended-stored-procedure-api.md)  
  
  
