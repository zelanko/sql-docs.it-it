---
title: Oggetti supportati dalla procedura guidata di generazione script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58e3aa77c7c21b89917c23c80f42330442863a18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063933"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Oggetti supportati dalla procedura guidata di generazione script
  La procedura guidata Genera e pubblica script supporta un subset degli oggetti supportati da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Oggetti supportati  
 Nella tabella seguente vengono elencati gli oggetti pubblicabili supportati dalla procedura guidata Genera e pubblica script.  
  
||||||  
|-|-|-|-|-|  
|Ruolo applicazione|Ruolo del database|schema|Aggregazione definita dall'utente|Visualizzazione<sup>1</sup>|  
|Assembly|Vincolo DEFAULT|Stored procedure di<sup>1</sup>|Tipo di dati definito dall'utente|Raccolta di XML Schema|  
|Vincolo CHECK|Catalogo full-text|Sinonimo|Funzione definita dall'utente||  
|Stored procedure CLR (common language runtime)<sup>1</sup>|Indice|Tabella|Tabella definita dall'utente||  
|Funzione CLR definita dall'utente|Regola|Utente<sup>2</sup>|Tipo definito dall'utente||  
  
 <sup>1</sup> pubblicato senza crittografia.  
  
 <sup>2</sup> qualsiasi utente non di sistema esistente nel database vengono pubblicati come ruoli.  
  
  
