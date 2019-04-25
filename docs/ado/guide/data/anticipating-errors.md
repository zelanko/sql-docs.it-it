---
title: Prevenzione degli errori | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91741ef8d6b0f7f984958837df3234b0bbc1e009
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472865"
---
# <a name="anticipating-errors"></a>Prevenzione degli errori
Prevenzione di errore è almeno tanto importante quanto la gestione degli errori. Questa sezione finale contiene un elenco ridotto di precauzioni che l'applicazione può richiedere per rendere meno probabile che si verificano errori.  
  
 Controllare lo stato degli oggetti controllando il valore **stato** proprietà prima di provare a eseguire un'operazione utilizzando gli oggetti. Ad esempio, se l'applicazione usa globale **connessione**, controllare relativo **stato** proprietà per verificare se è già aperta prima di chiamare il **aprire** (metodo).  
  
-   Qualsiasi programma che accetta i dati da un utente deve includere il codice per convalidare che i dati prima dell'invio all'archivio dati. Non è possibile utilizzare l'archivio dati, il provider, ADO o persino il linguaggio di programmazione per notificare eventuali problemi. È necessario controllare ogni singolo byte immesso dagli utenti, assicurandosi che i dati sono il tipo corretto per il campo e che i campi obbligatori non sono vuoti.  
  
 Controllare i dati prima di provare a scrivere dati nell'archivio dati. Il modo più semplice per eseguire questa operazione è per gestire il **WillMove** eventi o il **WillUpdateRecordset** evento. Per una descrizione più completa di gestione degli eventi ADO, vedere [gestione degli eventi ADO](../../../ado/guide/data/handling-ado-events.md).  
  
 Verificare che l'opzione **Recordset** gli oggetti non sono presenti oltre i limiti delle **Recordset** prima di provare a spostare il puntatore di record. Se si tenta **MoveNext** quando **EOF** è impostata su True o **MovePrev** quando **BOF** è True, si verificherà un errore. Se si esegue una delle **spostare** metodi quando entrambe **EOF** e **BOF** sono True, verrà generato un errore.  
  
 Errori si verificano anche se si prova a eseguire operazioni quali **Seek** e **trovare** su un oggetto vuoto **Recordset**.
