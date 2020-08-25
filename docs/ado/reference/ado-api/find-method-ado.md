---
description: Metodo Find (ADO)
title: Metodo Find (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: rothja
ms.author: jroth
ms.openlocfilehash: 0312fb8a8f91e8b56cb6c29a3a64b3a36bcec69d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775230"
---
# <a name="find-method-ado"></a>Metodo Find (ADO)
Esegue la ricerca di un [Recordset](./recordset-object-ado.md) per la riga che soddisfa i criteri specificati. Facoltativamente, è possibile specificare la direzione della ricerca, la riga iniziale e l'offset dalla riga iniziale. Se i criteri vengono soddisfatti, la posizione della riga corrente viene impostata sul record trovato; in caso contrario, la posizione viene impostata sull'estremità (o inizio) del **Recordset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Criteri*  
 Valore **stringa** che contiene un'istruzione che specifica il nome della colonna, l'operatore di confronto e il valore da utilizzare nella ricerca.  
  
 *SkipRows*  
 Facoltativa. Un valore **Long** , il cui valore predefinito è zero, che specifica l'offset di riga dalla riga corrente o dal segnalibro *Start* per iniziare la ricerca. Per impostazione predefinita, la ricerca viene avviata sulla riga corrente.  
  
 *SearchDirection*  
 Facoltativa. Valore [SearchDirectionEnum](./searchdirectionenum.md) che specifica se la ricerca deve iniziare sulla riga corrente o sulla riga successiva disponibile nella direzione della ricerca. Una ricerca non riuscita si interrompe alla fine del **Recordset** se il valore è **adSearchForward**. Una ricerca non riuscita viene arrestata all'inizio del **Recordset** se il valore è **adSearchBackward**.  
  
 *Inizia*  
 Facoltativa. Segnalibro **Variant** che funge da posizione iniziale per la ricerca.  
  
## <a name="remarks"></a>Commenti  
 Nei *criteri*è possibile specificare solo un nome di colonna singola. Questo metodo non supporta le ricerche su più colonne.  
  
 L'operatore di confronto nei *criteri* può essere " **>** " (maggiore di), "* * \<**" (less than), "=" (equal), "> =" (maggiore o uguale a), "<=" (minore o uguale a), "<>" (non uguale) o "like" (criteri di ricerca).  
  
 Il valore nei *criteri* può essere una stringa, un numero a virgola mobile o una data. I valori stringa sono delimitati da virgolette singole o "#" (simbolo di cancelletto), ad esempio "state =' WA '" o "state = #WA #". I valori di data sono delimitati dai contrassegni "#" (simbolo di cancelletto), ad esempio "start_date > #7/22/97 #". Questi valori possono contenere ore, minuti e secondi per indicare gli indicatori temporali, ma non devono contenere millisecondi o si verificheranno errori.  
  
 Se l'operatore di confronto è "like", il valore stringa può contenere un asterisco (*) per trovare una o più occorrenze di qualsiasi carattere o sottostringa. Ad esempio, "state like am" \* corrisponde a Maine e Massachusetts. È anche possibile usare gli asterischi iniziali e finali per trovare una sottostringa contenuta all'interno dei valori. Ad esempio, "state like ' \* As \* '" corrisponde a Alaska, Arkansas e Massachusetts.  
  
 Gli asterischi possono essere usati solo alla fine di una stringa di criteri o sia all'inizio che alla fine di una stringa di criteri, come illustrato in precedenza. Non è possibile usare l'asterisco come carattere jolly (' * Str ') principale o come carattere jolly incorporato (' \* s'). Verrà generato un errore.  
  
> [!NOTE]
>  Si verificherà un errore se non viene impostata una posizione della riga corrente prima di chiamare **Find**. Qualsiasi metodo che imposta la posizione della riga, ad esempio [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), deve essere chiamato prima di chiamare **Find**.  
  
> [!NOTE]
>  Se si chiama il metodo **Find** su un recordset e la posizione corrente nel recordset si trova all'ultimo record o alla fine del file (EOF), non sarà possibile trovare alcun valore. È necessario chiamare il metodo **MoveFirst** per impostare la posizione/il cursore corrente sull'inizio del recordset.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Find (VB)](./find-method-example-vb.md)   
 [Proprietà index](./index-property.md)   
 [Optimize Property-Dynamic (ADO)](./optimize-property-dynamic-ado.md)   
 [Metodo Seek](./seek-method.md)