---
title: srv_describe (API Stored procedure estesa) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_describe
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_describe
ms.assetid: 2115600e-5ce7-4be0-9cd3-a1dd1fab0729
author: rothja
ms.author: jroth
ms.openlocfilehash: f8904e3c08789eb0cb50b0f5a20b66c851578ac5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064117"
---
# <a name="srv_describe-extended-stored-procedure-api"></a>srv_describe (API Stored procedure estesa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Definisce il nome della colonna e i tipi di dati di origine e di destinazione per una colonna specifica in una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
int srv_describe (  
SRV_PROC *  
srvproc  
,  
int  
colnumber  
,  
DBCHAR *  
column_name  
,  
int  
namelen  
,  
DBINT  
desttype  
,  
DBINT  
destlen  
,  
DBINT  
srctype  
,  
DBINT  
srclen  
,  
void *  
srcdata  
);  
```  
  
## <a name="arguments"></a>Argomenti  
 *srvproc*  
 Puntatore alla struttura SRV_PROC che rappresenta l'handle di una determinata connessione client, in questo caso il client che invia la riga. La struttura contiene tutte le informazioni utilizzate dalla libreria dell'API della stored procedure estesa per gestire le comunicazioni e i dati tra l'applicazione e il client.  
  
 *colnumber*  
 Attualmente non supportato. Le colonne devono essere descritte in ordine. Tutte le colonne devono essere descritte prima che venga chiamata **srv_sendrow**.  
  
 *column_name*  
 Specifica il nome della colonna a cui appartengono i dati. Questo parametro può essere NULL in quanto una colonna non deve necessariamente avere un nome.  
  
 *namelen*  
 Specifica la lunghezza, espressa in byte, di *column_name*. Se *namelen* è SRV_NULLTERM, *column_name* deve essere con terminazione Null.  
  
 *destType*  
 Specifica il tipo di dati della colonna della riga di destinazione. Si tratta del tipo di dati inviato al client. È necessario specificarlo anche se i dati sono NULL. Per altre informazioni, vedere [Tipi di dati &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
 *destlen*  
 Specifica la lunghezza, espressa in byte, dei dati da inviare al client. Per tipi di dati a lunghezza fissa che non consentono i valori Null, *destlen* viene ignorato. Per tipi di dati a lunghezza variabile e a lunghezza fissa che consentono i valori Null, *destlen* specifica la lunghezza massima dei dati di destinazione.  
  
 *srcType*  
 Specifica il tipo di dati dei dati di origine.  
  
 *srclen*  
 Specifica la lunghezza, espressa in byte, dei dati di origine. Questo valore viene ignorato per i tipi di dati a lunghezza fissa.  
  
 *srcdata*  
 Fornisce l'indirizzo dei dati di origine per una determinata colonna. Dopo essere stata chiamata, **srv_sendrow** cerca i dati di *colnumber* in *srcdata*. È necessario quindi non liberarlo prima di una chiamata a **srv_sendrow**. L'indirizzo dei dati di origine può essere modificato tra una chiamata e l'altra a **srv_sendrow** usando **srv_setcoldata**. La memoria allocata per *srcdata* non deve essere liberata fino a quando i dati della colonna non vengono sostituiti da un'altra chiamata a **srv_setcoldata** o fino alla chiamata a **srv_senddone**.  
  
 Se *desttype* è SRVDECIMAL o SRVNUMERIC, il parametro *srcdata* deve essere un puntatore a una struttura DBNUMERIC o DBDECIMAL con i campi della precisione e della scala della struttura già impostati sui valori desiderati. È possibile utilizzare DEFAULTPRECISION per specificare una precisione predefinita e DEFAULTSCALE per specificare una scala predefinita.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Il numero della colonna descritta. La prima colonna è la colonna 1. Se si verifica un errore, viene restituito 0.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **srv_describe** deve essere chiamata una volta per ogni colonna nella riga prima della prima chiamata a **srv_sendrow**. Le colonne di una riga possono essere descritte in qualsiasi ordine.  
  
 Per modificare il percorso e lunghezza dei dati di origine nelle righe della colonna prima dell'invio del set di risultati completo, usare rispettivamente **srv_setcoldata** e **srv_setcollen**.  
  
 Per una descrizione dei tipi di dati e delle conversioni dei tipi di dati dell'API Stored procedure estesa, vedere [Tipi di dati &#40;API Stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md).  
  
 Se il nome della colonna nell'applicazione è in Unicode, è necessario convertirlo nella tabella codici multibyte del server prima di chiamare **srv_describe**. Per altre informazioni, vedere [Dati Unicode e tabelle codici del server](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md).  
  
> [!IMPORTANT]  
>  È necessario esaminare con attenzione il codice sorgente delle stored procedure estese e testare le DLL compilate prima di installarle in un server di produzione. Per informazioni sui test e sull'analisi della sicurezza, visitare questo [sito Web Microsoft](https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vedere anche  
 [srv_sendrow &#40;API stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-sendrow-extended-stored-procedure-api.md)   
 [srv_setutype &#40;API stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)   
 [srv_setcoldata &#40;API stored procedure estesa&#41;](../../relational-databases/extended-stored-procedures-reference/srv-setcoldata-extended-stored-procedure-api.md)  
  
  
