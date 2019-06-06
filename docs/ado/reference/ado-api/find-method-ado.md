---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3f544ae5a38b50ed13ddbafb725c07e0c8a4c8e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697960"
---
# <a name="find-method-ado"></a>Metodo Find (ADO)
Cerca un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) per la riga che soddisfa i criteri specificati. Facoltativamente, può essere specificata la direzione della ricerca, la riga iniziale e offset della riga iniziale. Se vengono soddisfatti i criteri, la posizione della riga corrente è impostata sul record trovato. in caso contrario, la posizione è impostata su finale (o avvio) del **Recordset**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Criteri*  
 Oggetto **stringa** valore contenente un'istruzione che specifica il nome della colonna, l'operatore di confronto e valore da utilizzare nella ricerca.  
  
 *SkipRows*  
 Facoltativo *.* Oggetto **lungo** valore, il cui valore predefinito è zero, che specifica l'offset di riga rispetto alla riga corrente oppure *avviare* segnalibro per iniziare la ricerca. Per impostazione predefinita, verrà avviata la ricerca nella riga corrente.  
  
 *SearchDirection*  
 Facoltativo *.* Oggetto [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) valore che specifica se la ricerca inizierà nella riga corrente o la successiva riga disponibile nella direzione della ricerca. Arresta una ricerca in fondo il **Recordset** se il valore è **adSearchForward**. Arresta una ricerca all'inizio del **Recordset** se il valore è **adSearchBackward**.  
  
 *Start*  
 Facoltativo. Oggetto **Variant** segnalibro che funziona come la posizione iniziale per la ricerca.  
  
## <a name="remarks"></a>Note  
 Solo un nome di colonna singola può essere specificato *criteri*. Questo metodo non supporta le ricerche su più colonne.  
  
 L'operatore di confronto *criteri* potrebbe essere " **>** "(maggiore)," **\<** " (minore di), "=" (uguale), "> =" (maggiore o uguale), "< =" (minore o uguale a), "<>" (non uguale), o "like" (criteri di ricerca).  
  
 Il valore in *criteri* potrebbe essere una stringa, numero a virgola mobile o Data. Valori stringa sono delimitati da virgolette singole o doppie "" cancelletto (#) (ad esempio, "stato ="WA"" o "state = WA # #"). I valori delle date sono delimitati con segni di (cancelletto) "#" (ad esempio, "start_date > & 97/n. 7/22"). Questi valori possono contenere ore, minuti e secondi per indicare i timbri data / ora, ma non devono contenere millisecondi o si verificheranno errori.  
  
 Se l'operatore di confronto è "like", il valore della stringa può contenere un asterisco (*) per trovare una o più occorrenze di qualsiasi carattere o una sottostringa. Ad esempio, "stato come sto\*'" corrisponde a Maine e Massachusetts. È possibile utilizzare anche gli asterischi iniziali e finali per trovare una sottostringa contenuta all'interno dei valori. Ad esempio, "stato, ad esempio '\*come\*'" corrisponde a Alaska Arkansas e Massachusetts.  
  
 Gli asterischi sono utilizzabile solo alla fine di una stringa di criteri o all'inizio e fine di una stringa di criteri, come illustrato in precedenza. È possibile usare l'asterisco come carattere jolly iniziale ('* str'), o come un carattere jolly incorporati di s\*r'). Ciò causerà un errore.  
  
> [!NOTE]
>  Si verifica un errore se una posizione della riga corrente non è impostata prima di chiamare **trovare**. Qualsiasi metodo che imposta la posizione di riga, ad esempio [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), deve essere chiamato prima di chiamare **trovare**.  
  
> [!NOTE]
>  Se si chiama il **trovare** metodo su un set di record e la posizione corrente nel set di record è all'ultimo record o alla fine del file (EOF), non sarà possibile trovare alcuna operazione. È necessario chiamare il **MoveFirst** metodo per impostare il cursore/posizione corrente all'inizio del set di record.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo Find (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Proprietà index](../../../ado/reference/ado-api/index-property.md)   
 [Ottimizzare la proprietà dinamica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Metodo Seek](../../../ado/reference/ado-api/seek-method.md)
