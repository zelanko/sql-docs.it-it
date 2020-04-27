---
title: Modificare le stored procedure che utilizzano proprietà della ricerca full-text obsolete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093847"
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
  
## <a name="see-also"></a>Vedi anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
