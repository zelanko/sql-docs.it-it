---
title: Disconnessione e riconnessione del recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9829ddfd7e625941c97bd3b2027c328a1fba93d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925517"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Disconnessione e riconnessione del recordset
Una delle funzionalità più potenti disponibili in ADO è la possibilità di aprire un recordset lato client da un'origine dati e quindi di disconnettere il recordset dall'origine dati. Una volta che il recordset è stato disconnesso, è possibile chiudere la connessione all'origine dati, rilasciando quindi le risorse sul server usato per gestirlo. È possibile continuare a visualizzare e modificare i dati nel recordset mentre è disconnesso e successivamente riconnettersi all'origine dati e inviare gli aggiornamenti in modalità batch.  
  
 Per disconnettere un recordset, aprirlo con una posizione del cursore adUseClient, quindi impostare la proprietà ActiveConnection su Nothing. (Gli utenti C++ devono impostare ActiveConnection su NULL per disconnettersi).  
  
 Si userà un recordset disconnesso più avanti in questa sezione quando si discute la persistenza dei recordset per risolvere uno scenario in cui è necessario che i dati di un recordset siano disponibili per un'applicazione mentre il computer client non è connesso a una rete.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
