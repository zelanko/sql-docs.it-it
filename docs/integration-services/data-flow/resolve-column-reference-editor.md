---
description: Editor della risoluzione dei riferimenti alle colonne
title: Editor della risoluzione dei riferimenti alle colonne | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3610ee6cd8a2033a67c23051ca3bd47952ac318f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484531"
---
# <a name="resolve-column-reference-editor"></a>Editor della risoluzione dei riferimenti alle colonne

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando un percorso di input viene disconnesso o se contiene colonne senza mapping, viene visualizzata un'icona di errore accanto al percorso di dati corrispondente. Per semplificare la risoluzione degli errori di riferimento alle colonne, l'editor per la risoluzione dei riferimenti consente di collegare le colonne di output senza mapping alle colonne di input senza mapping per tutti i percorsi nell'albero di esecuzione. Nell'editor per la risoluzioni dei riferimenti verranno inoltre evidenziati i percorsi risolti.  
  
> [!NOTE]  
>  È possibile modificare un componente anche quando il relativo percorso di input è disconnesso  
  
 Dopo che sono stati risolti tutti i riferimenti alle colonne, in assenza di altri errori del percorso dati, accanto al percorso dati non verranno più visualizzate altre icone di errore.  
  
## <a name="options"></a>Opzioni  
 **Colonne di output senza mapping (Origine)**     
 Colonne del percorso a monte di cui non è stato eseguito il mapping  
  
**Colonne con mapping (Origine)**     
 Colonne del percorso a monte di cui è stato eseguito il mapping alle colonne del percorso a valle  
  
**Colonne con mapping (Destinazione)**     
 Colonne del percorso a monte di cui è stato eseguito il mapping alle colonne del percorso a valle  
  
**Colonne di input senza mapping (Destinazione)**     
 Colonne del percorso a valle di cui non è stato eseguito il mapping  
  
**Elimina colonne input senza mapping**  
 Selezionare Elimina colonne input senza mapping per ignorare le colonne senza mapping alla destinazione del percorso dati. Il pulsante Anteprima modifiche consente di visualizzare un elenco delle modifiche che si verificheranno alla pressione del pulsante OK.  
  
  
