---
title: Opzioni (pagina ANSI) l'esecuzione di query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d9a8b5dea5ab90137c95c9ddaf609c63532dd5b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089076"
---
# <a name="query-options-execution-ansi-page"></a>Esecuzione di Opzioni query (pagina ANSI)
  Questa pagina consente di indicare se [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debba eseguire le query usando tutte o una parte delle impostazioni specificate nello standard ISO (ANSI).  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **SET ANSI_DEFAULTS**  
 Consente di selezionare tutte le impostazioni ISO predefinite. Per impostazione predefinita, la casella non è disponibile perché solo alcune impostazioni ISO sono configurate.  
  
 **SET QUOTED_IDENTIFIER**  
 Consente di racchiudere gli identificatori di oggetto tra virgolette. Questa opzione è selezionata per impostazione predefinita.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Consente l'uso di valori Null per ogni colonna o tipo di dati definito dall'utente non indicato in modo esplicito come NOT NULL, lo stato predefinito, durante un'istruzione CREATE TABLE o ALTER TABLE. Questa opzione è selezionata per impostazione predefinita.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Consente di chiudere automaticamente tutti i cursori aperti (in conformità alla specifica ISO) quando viene eseguito il commit di una transazione. Se questa opzione è deselezionata, ovvero impostata su OFF, i cursori rimangono aperti durante la transazione e vengono chiusi solo con un comando esplicito o quando viene chiusa la connessione. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET ANSI_PADDING**  
 Controlla il modo in cui la colonna archivia i valori di dimensioni inferiori a quelle definite della colonna e i valori contenenti spazi vuoti finali nei dati **char**, **varchar**, **binary**e **varbinary** . Questa impostazione influisce solo sulla definizione di nuove colonne. Dopo la creazione della colonna, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] archivia i valori in base all'impostazione specificata in fase di creazione. Le successive modifiche dell'impostazione non influiscono sulle colonne esistenti. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET ANSI_WARNINGS**  
 Specifica il funzionamento standard ISO in varie condizioni di errore.  
  
-   Se questa casella di controllo è selezionata e le funzioni di aggregazione, ad esempio SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP o COUNT, includono valori Null, viene generato un messaggio di avviso. Se l'opzione è impostata su **OFF**, non viene generato alcun messaggio di avviso.  
  
-   Quando questa casella di controllo è deselezionata, viene eseguito il rollback dell'istruzione e visualizzato un messaggio di errore a seguito di errori di divisione per zero e di overflow aritmetico. Quando è impostata su OFF, a seguito di errori di divisione per zero e di overflow aritmetico vengono restituiti valori Null. Un errore di divisione per zero o di overflow aritmetico si verifica se viene eseguita un'operazione INSERT o UPDATE in una colonna di tipo character, Unicode o binary in cui la lunghezza di un nuovo valore supera le dimensioni massime della colonna. Se l'opzione **SET ANSI_WARNINGS** è impostata su ON, l'operazione INSERT o UPDATE viene annullata, come specificato dallo standard ISO. Nelle colonne di testo vengono ignorati gli spazi vuoti finali, mentre nelle colonne binarie vengono ignorati i valori finali Null. Quando l'opzione è impostata su OFF, i dati vengono troncati in base alle dimensioni della colonna e l'istruzione ha esito positivo.  
  
 Questa opzione è selezionata per impostazione predefinita.  
  
 **SET ANSI_NULLS**  
 Consente di specificare il funzionamento conforme allo standard ISO degli operatori di confronto Uguale a (`=`) e Diverso da (`<>`) quando questi vengono utilizzati con valori Null. Quando **SET ANSI_NULLS** è selezionata, tutti i confronti con un valore Null restituiscono UNKNOWN, in conformità allo standard ISO. Quando l'opzione **SET ANSI_NULLS** non è selezionata, i confronti di tutti i dati con un valore Null restituiscono TRUE, se il valore dei dati è NULL. Questa opzione è selezionata per impostazione predefinita.  
  
 **Ripristina predefiniti**  
 Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.  
  
  
