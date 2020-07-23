---
title: Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.suggestdatatypes.f1
ms.assetid: 8d5652e0-cf57-483f-828b-10f00c08418b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a1e742bfc0254cddf38a73a8b5923168fb58745f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918251"
---
# <a name="suggest-column-types-dialog-box-ui-reference"></a>Riferimento all'interfaccia utente della finestra di dialogo Suggerisci tipi di colonne

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la finestra di dialogo **Suggerisci tipi di colonne** per identificare il tipo di dati e la lunghezza delle colonne nella gestione connessione file flat sulla base di un campionamento del contenuto del file.  
  
 Per altre informazioni sui tipi di dati usati da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="options"></a>Opzioni  
 **Numero di righe**  
 Consente di digitare o selezionare il numero di righe nel campione utilizzato dall'algoritmo.  
  
 **Suggerisci tipo di dati integer più piccolo**  
 Deselezionare questa casella di controllo per ignorare la valutazione. Se questa casella di controllo è selezionata, viene determinato il tipo di dati integer più piccolo possibile per le colonne che contengono dati numerici integrali.  
  
 **Suggerisci tipo di dati real più piccolo**  
 Deselezionare questa casella di controllo per ignorare la valutazione. Se questa casella di controllo è selezionata, viene determinato se le colonne contenenti dati numerici real possono utilizzare il tipo di dati real più piccolo, ovvero DT_R4.  
  
 **Identifica colonne booleane con i valori seguenti**  
 Consente di digitare i due valori che si desidera utilizzare come valori booleani true e false. Digitare i valori separati da una virgola. Il primo valore rappresenta il valore True.  
  
 **Consenti riempimento colonne stringa**  
 Selezionare questa casella di controllo per attivare il riempimento della stringa.  
  
 **Percentuale di riempimento**  
 Consente di digitare o selezionare la percentuale della lunghezza delle colonne in base alla quale deve essere aumentata la lunghezza delle colonne per i tipi di dati character. La percentuale deve essere un numero intero.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Gestione connessione file flat](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
