---
title: Provider di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 30d1e1515ed3e84640fe1ca004cb7cbf4383ce97
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718721"
---
# <a name="data-providers"></a>Provider di dati
Provider di dati rappresentano diverse origini dei dati, ad esempio database SQL, file sequenziali-indicizzate, fogli di calcolo, archivi di documenti e i file di posta elettronica. I provider di espongono i dati in modo uniforme tramite un'astrazione comune definita set di righe.  
  
 ADO è potente e flessibile perché può connettersi a una qualsiasi di diversi provider di dati diversi e ancora esporre il modello di programmazione stesso, indipendentemente dalle funzionalità specifiche di qualsiasi altro provider specificato. Tuttavia, poiché ogni provider di dati è univoco, come l'applicazione interagisce con ADO dipendono dal provider di dati.  
  
 Ad esempio, le funzionalità e caratteristiche del Provider OLE DB per SQL Server, che viene usato per accedere ai database Microsoft SQL Server, sono considerevolmente diverse da quelle di Provider Microsoft OLE DB per Internet Publishing, che consente di accedere ai file archivi in un server Web.
