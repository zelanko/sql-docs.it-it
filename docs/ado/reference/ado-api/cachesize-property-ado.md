---
title: Esempio di proprietà CacheSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76cd9e4977ffda023c270a027602597ddf7b9a4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028228"
---
# <a name="cachesize-property-ado"></a>Proprietà CacheSize (ADO)
Indica il numero di record restituiti da una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti memorizzati localmente nella memoria.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che deve essere maggiore di 0. Valore predefinito è 1.  
  
## <a name="remarks"></a>Note  
 Usare la **CacheSize** proprietà per controllare il numero di record per recuperare in una sola volta nella memoria locale del provider. Ad esempio, se il **CacheSize** è 10, dopo l'apertura prima le **Recordset** dell'oggetto, il provider recupera i primi 10 record nella memoria locale. Quando si spostano attraverso la **Recordset** dell'oggetto, il provider restituisce i dati dal buffer di memoria locale. Non appena si sposta oltre l'ultimo record nella cache, il provider recupera i successivi 10 record dall'origine dati nella cache.  
  
> [!NOTE]
>  **CacheSize** si basa sul **numero massimo righe aperte** proprietà specifiche del provider (nel **le proprietà** insieme del **Recordset** oggetto). Non è possibile impostare **CacheSize** su un valore maggiore **numero massimo righe aperte**. Per modificare il numero di righe che può essere aperta dal provider, impostare **numero massimo righe aperte**.  
  
 Il valore di **CacheSize** può essere modificata nel corso della durata delle **Recordset** oggetto, ma se si modifica questo valore interessa solo il numero di record nella cache dopo recuperi successivi, dall'origine dati. La modifica il valore della proprietà da solo non modificherà il contenuto corrente della cache.  
  
 Se sono presenti record minore rispetto al recupero **CacheSize** specifica, il provider restituisce i record rimanenti e si verifica alcun errore.  
  
 Oggetto **CacheSize** impostando pari a zero non è consentito e restituisce un errore.  
  
 I record recuperati dalla cache non riflettono le modifiche simultanee che altri utenti apportate ai dati di origine. Per forzare un aggiornamento di tutti i dati memorizzati nella cache, usare il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) (metodo).  
  
 Se **CacheSize** è impostata su un valore maggiore di uno, i metodi di navigazione ([spostare](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) potrebbe causare il passaggio a un eliminare record, se l'eliminazione viene eseguita dopo che sono stati recuperati i record. Dopo l'operazione di recupero iniziale, le successive operazioni di eliminazione non si rifletteranno nella cache per i dati fino a quando non si tenta di accedere a un valore di dati da una riga eliminata. Tuttavia, impostando **CacheSize** uno consente di eliminare questo problema poiché non è possibile recuperare le righe eliminate.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà CacheSize (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [Esempio di proprietà CacheSize (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [Esempio di proprietà CacheSize (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
