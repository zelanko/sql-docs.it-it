---
title: Oggetti supportati dalla procedura guidata di generazione script
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c266cf82a6f790d20cec3b3ec94f3c5e42b74b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75241986"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>Oggetti supportati dalla procedura guidata di generazione script
  La procedura guidata Genera e pubblica script supporta un subset degli oggetti supportati da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="supported-objects"></a>Oggetti supportati  
 Nella tabella seguente vengono elencati gli oggetti pubblicabili supportati dalla procedura guidata Genera e pubblica script.  
  
||||||  
|-|-|-|-|-|  
|Ruolo applicazione|Ruolo del database|SCHEMA|Aggregazione definita dall'utente|Visualizzazione<sup>1</sup>|  
|Assembly|Vincolo DEFAULT|Stored procedure<sup>1</sup>|Tipo di dati definito dall'utente|Raccolta di XML Schema|  
|Vincolo CHECK|Catalogo full-text|Sinonimo|Funzione definita dall'utente||  
|CLR (Common Language Runtime) stored procedure<sup>1</sup>|Indice|Tabella|Tabella definita dall'utente||  
|Funzione CLR definita dall'utente|Regola|Utente<sup>2</sup>|Tipo definito dall'utente||  
  
 <sup>1</sup> pubblicato senza crittografia.  
  
 <sup>2</sup> qualsiasi utente non di sistema esistente nel database viene pubblicato come ruolo.  
  
  
