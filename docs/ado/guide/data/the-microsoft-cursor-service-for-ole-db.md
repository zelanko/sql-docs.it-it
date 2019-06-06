---
title: Microsoft Cursor Service per OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbf289e73cd3cb94418521f3d4070cf155a7fdf2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704919"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>Microsoft Cursor Service per OLE DB
Quando si seleziona un cursore lato client, o impostare il **CursorLocation** proprietà **adUseClient**, si è chiamando il Microsoft Cursor Service per OLE DB. È anche possibile visualizzare i riferimenti per il "Client motore del cursore", che è essenzialmente la stessa operazione nel contesto di ADO. Questo servizio integra le funzioni di cursore-supporto del provider di dati. Di conseguenza, è possibile percepire funzionalità relativamente uniforme di tutti i provider di dati.  
  
 Cursor Service per OLE DB rende disponibili le proprietà dinamiche e migliora il comportamento di determinati metodi. Ad esempio, il **Ottimizza** proprietà dinamica consente la creazione di indici temporanei per rendere alcune operazioni, ad esempio le **trovare** (metodo).  
  
 Il servizio di cursore Abilita il supporto per l'aggiornamento in batch in tutti i casi. Simula anche in grado di supportare più tipi di cursore, ad esempio i cursori dynamic, quando un provider di dati possa fornire solo i cursori meno efficienti, ad esempio i cursori statici.  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Cursor Service per OLE DB (componente servizio ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
