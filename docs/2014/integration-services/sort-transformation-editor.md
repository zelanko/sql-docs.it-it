---
title: Editor trasformazione ordinamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort Transformation Editor
ms.assetid: 8ae23970-49a9-4d6d-9f15-c7074783347c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: becd97e843909a5d7bc181dfdf1060988836ee3b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055489"
---
# <a name="sort-transformation-editor"></a>Editor trasformazione Ordinamento
  Utilizzare la finestra di dialogo **Editor trasformazione Ordinamento** per selezionare le colonne da ordinare, impostare il tipo di ordinamento e specificare se rimuovere i duplicati.  
  
 Per ulteriori informazioni sulla trasformazione Ordinamento, vedere [Sort Transformation](data-flow/transformations/sort-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di specificare le colonne da ordinare utilizzando le caselle di controllo.  
  
 **Nome**  
 Consente di visualizzare il nome di ogni colonna di input disponibile.  
  
 **Pass-through**  
 Indica se includere la colonna nell'output ordinato.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili per ogni riga. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo nella tabella **Colonne di input disponibili** .  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Tipo di ordinamento**  
 Indica se eseguire l'ordinamento in ordine crescente o decrescente.  
  
 **Ordinamento**  
 Indica l'ordine da utilizzare per l'ordinamento delle colonne. È possibile impostare questa opzione in modo manuale per ogni colonna.  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](data-flow/comparing-string-data.md).  
  
 **Rimuovi righe con valori di ordinamento duplicati**  
 Indica se la trasformazione copia le righe duplicate nell'output della trasformazione o se invece crea un'unica voce per tutti i duplicati in base alla stringa specificata nelle opzioni di confronto.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
