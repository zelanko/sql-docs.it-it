---
title: Editor trasformazione Ricerca fuzzy (scheda colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.columns.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76bac38991d30c566c988beba7d806f35e107b23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768103"
---
# <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>Editor trasformazione Ricerca fuzzy (scheda Colonne)
  Utilizzare la scheda **Colonne** della finestra di dialogo **Editor trasformazione Ricerca fuzzy** per impostare le proprietà delle colonne di input e output.  
  
 Per ulteriori informazioni sulla trasformazione Ricerca fuzzy, vedere [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Trascinare le colonne di input per collegarle alle colonne di ricerca disponibili. Queste colonne devono disporre di tipi di dati supportati e corrispondenti. Selezionare una riga di mapping e fare clic con il pulsante destro del mouse per modificare i mapping nella finestra di dialogo [Crea relazioni](data-flow/transformations/create-relationships.md) .  
  
 **Name**  
 Consente di visualizzare i nomi delle colonne di input disponibili.  
  
 **Pass-through**  
 Consente di indicare l'inclusione delle colonne di input nell'output della trasformazione.  
  
 **Colonne di ricerca disponibili**  
 Utilizzare le caselle di controllo per selezionare le colonne su cui eseguire operazioni di ricerca fuzzy.  
  
 **Colonna di ricerca**  
 Selezionare le colonne di ricerca dall'elenco delle colonne della tabella di riferimento disponibili. Queste selezioni si rifletteranno nelle selezioni delle caselle di controllo nella tabella **Colonne di ricerca disponibili** . La selezione di una colonna nella tabella **Colonne di ricerca disponibili** comporta la creazione di una colonna di output contenente il valore della colonna della tabella di riferimento per ogni riga corrispondente restituita.  
  
 **Alias di output**  
 Consente di digitare un alias per l'output relativo a ogni colonna di ricerca. Per impostazione predefinita viene suggerito il nome della colonna di ricerca a cui è accodato un valore di indice numerico. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda Tabella di riferimento&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor trasformazione Ricerca fuzzy &#40;scheda Avanzate&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
