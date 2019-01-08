---
title: Editor trasformazione ricerca (pagina avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2991d6b79c9cbfbd37466484e1c4394b6e0fb804
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369363"
---
# <a name="lookup-transformation-editor-advanced-page"></a>Editor trasformazione Ricerca (pagina Avanzate)
  La pagina **Avanzate** della finestra di dialogo **Editor trasformazione Ricerca** consente di configurare la memorizzazione nella cache parziale e di modificare l'istruzione SQL della trasformazione Ricerca.  
  
 Per ulteriori informazioni sulla trasformazione Ricerca, vedere [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Dimensioni cache (32 bit)**  
 Consente di regolare le dimensioni della cache (in megabyte) per i computer a 32 bit. Il valore predefinito è 5 MB.  
  
 **Dimensioni cache (64 bit)**  
 Consente di regolare le dimensioni della cache (in megabyte) per i computer a 64 bit. Il valore predefinito è 5 MB.  
  
 **Attivare cache per righe senza voci corrispondenti**  
 Consente di memorizzare nella cache le righe senza voci corrispondenti nel set di dati di riferimento.  
  
 **Allocazione dalla cache**  
 Consente di specificare la percentuale della cache da allocare per le righe senza voci corrispondenti nel set di dati di riferimento.  
  
 **Modifica istruzione SQL**  
 Consente di modificare l'istruzione SQL utilizzata per generare il set di dati di riferimento.  
  
> [!NOTE]  
>  L'istruzione SQL facoltativa specificata in questa pagina sostituisce il nome tabella specificato nella pagina **Connessione** di **Editor trasformazione Ricerca**. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Connessione&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md).  
  
 **Impostazione dei parametri**  
 Consente di eseguire il mapping delle colonne di input ai parametri mediante la finestra di dialogo **Imposta parametri query** .  
  
## <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://go.microsoft.com/fwlink/?LinkId=219518) su blogs.msdn.com  
  
## <a name="see-also"></a>Vedere anche  
 [Editor trasformazione Ricerca &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor trasformazione Ricerca &#40;pagina Connessione&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Colonne&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Trasformazione Ricerca fuzzy](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
