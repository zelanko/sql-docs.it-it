---
title: Uso di CacheSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d0b6a1b83b09d504f8f3394a32ee10d556fcd18c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699734"
---
# <a name="using-cachesize"></a>Uso di CacheSize
Usare la **CacheSize** proprietà per controllare il numero di record per recuperare in una sola volta nella memoria locale del provider. Ad esempio, se il **CacheSize** è 10, dopo l'apertura prima le **Recordset** dell'oggetto, il provider recupera i primi 10 record nella memoria locale. Quando si spostano attraverso la **Recordset** dell'oggetto, il provider restituisce i dati dal buffer di memoria locale. Non appena si sposta oltre l'ultimo record nella cache, il provider recupera i successivi 10 record dall'origine dati nella cache.  
  
> [!NOTE]
>  **CacheSize** si basa sul **numero massimo righe aperte** proprietà specifiche del provider (nel **le proprietà** insieme del **Recordset** oggetto). Non è possibile impostare **CacheSize** su un valore maggiore **numero massimo di righe aperto.** Per modificare il numero di righe che può essere aperto dal provider, impostare **numero massimo righe aperte**.  
  
 Il valore di **CacheSize** può essere modificata nel corso della durata delle **Recordset** oggetto, ma se si modifica questo valore interessa solo il numero di record nella cache dopo recuperi successivi, dall'origine dati. La modifica il valore della proprietà da solo non modificherà il contenuto corrente della cache.  
  
 Se sono presenti record minore rispetto al recupero **CacheSize** specifica, il provider restituisce i record rimanenti e si verifica alcun errore.  
  
 Oggetto **CacheSize** impostando pari a zero non è consentito e restituisce un errore.  
  
 Record recuperato dalla cache non riflettono le modifiche simultanee che altri utenti apportate ai dati di origine. Per forzare un aggiornamento di tutti i dati memorizzati nella cache, usare il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) (metodo).  
  
 Se **CacheSize** è impostata su un valore maggiore di 1, i metodi di navigazione ([spostare](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) potrebbe causare il passaggio a una classe eliminata registrare, se l'eliminazione viene eseguita dopo che sono stati recuperati i record. Dopo l'operazione di recupero iniziale, le successive operazioni di eliminazione non si rifletteranno nella cache per i dati fino a quando non si tenta di accedere a un valore di dati da una riga eliminata. Tuttavia, impostando **CacheSize** a 1 consente di eliminare questo problema in quanto non è possibile recuperare le righe eliminate.
