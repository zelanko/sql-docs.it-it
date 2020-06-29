---
title: Editor trasformazione Raggruppamento fuzzy (scheda Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.connection.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b2a8b0af9f36fdd386f7da375184fd4e4ec5c4be
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425298"
---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor trasformazione Raggruppamento fuzzy (scheda Gestione connessione)
  Utilizzare la scheda **Gestione connessione** della finestra di dialogo **Editor trasformazione Raggruppamento fuzzy** per selezionare una connessione esistente o crearne una nuova.  
  
> [!NOTE]  
>  Sul server specificato dalla connessione deve essere in esecuzione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La trasformazione Raggruppamento fuzzy crea in tempdb oggetti dati temporanei che possono avere le stesse dimensioni dell'intero input della trasformazione. Durante l'esecuzione della trasformazione vengono eseguite query del server su tali oggetti temporanei. Queste query possono influire sulle prestazioni generali del server.  
  
 Per ulteriori informazioni sulla trasformazione Raggruppamento fuzzy, vedere [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione OLE DB**  
 Consente di selezionare una gestione connessione OLE DB esistente usando la casella di riepilogo o di creare una nuova connessione tramite il pulsante **Nuova** .  
  
 **Nuovo**  
 Consente di creare una nuova connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificazione di righe di dati simili tramite la trasformazione Raggruppamento fuzzy](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
