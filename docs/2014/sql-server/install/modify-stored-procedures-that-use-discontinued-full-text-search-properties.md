---
title: Modificare le stored procedure che utilizzano proprietà di ricerca Full-Text obsolete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d6d7467da572d5d0552d400e2c05505c1bc0aaa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267554"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>Modificare le stored procedure che utilizzano proprietà della ricerca full-text obsolete
  Per garantire la corretta esecuzione delle stored procedure, modificare le procedure esistenti e rimuovere le proprietà e le impostazioni relative alla ricerca full-text che sono state rimosse o deprecate.  
  
## <a name="component"></a>Componente  
 Ricerca full-text  
  
## <a name="description"></a>Descrizione  
 Le seguenti proprietà e impostazioni relative alla ricerca full-text sono state rimosse.  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 Le seguenti proprietà e impostazioni relative alla ricerca full-text sono state rimosse o deprecate:  
  
-   Percorso del catalogo full-text. Il catalogo full-text è un oggetto logico senza un percorso di file specifico nel sistema.  
  
-   L'attivazione/disabilitazione in SP_FULLTEXT_DATABASE non ha più effetto, poiché i database sono sempre attivati per la ricerca full-text e per impostazione predefinita in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le stored procedure per rimuovere queste proprietà.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
