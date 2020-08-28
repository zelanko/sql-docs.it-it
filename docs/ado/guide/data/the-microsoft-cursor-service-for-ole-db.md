---
description: Microsoft Cursor Service per OLE DB
title: Il servizio Microsoft Cursor per OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: rothja
ms.author: jroth
ms.openlocfilehash: ce59aa28e8db4716b0e27c848ce774b489ff5891
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979372"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>Microsoft Cursor Service per OLE DB
Quando si seleziona un cursore sul lato client o si imposta la proprietà **CursorLocation** su **adUseClient**, viene richiamato il servizio Microsoft Cursor per OLE DB. È anche possibile visualizzare i riferimenti al "motore di cursori client", che è essenzialmente la stessa cosa nel contesto di ADO. Questo servizio integra le funzioni di supporto del cursore dei provider di dati. Di conseguenza, è possibile percepire funzionalità relativamente uniformi da tutti i provider di dati.  
  
 Il servizio Cursor per OLE DB rende disponibili le proprietà dinamiche e migliora il comportamento di alcuni metodi. Ad esempio, la proprietà **ottimizza** dinamica consente la creazione di indici temporanei per facilitare determinate operazioni, ad esempio il metodo **Find** .  
  
 Il servizio Cursor Abilita il supporto per l'aggiornamento in batch in tutti i casi. Simula inoltre tipi di cursore più idonei, ad esempio cursori dinamici, quando un provider di dati può fornire solo cursori meno idonei, ad esempio i cursori statici.  
  
## <a name="see-also"></a>Vedere anche  
 [Servizio Microsoft Cursor per OLE DB (componente servizio ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
