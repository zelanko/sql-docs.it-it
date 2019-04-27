---
title: Proprietà catalogo full-Text (pagina tabelle e viste) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 78d7dc111bc0b6eb10e80f32785beeda710e52bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779192"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>Proprietà catalogo full-text (pagina Tabelle e viste)
  Utilizzare questa finestra di dialogo per visualizzare o modificare le tabelle e le viste assegnate al catalogo full-text.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Tutti gli oggetti tabella/vista idonei nel database**  
 Elenca le tabelle e le viste che hanno un indice univoco definito, ma che non fanno già parte del catalogo full-text. Per selezionare una tabella o vista e assegnarla al catalogo, selezionare gli elementi nella casella di riepilogo e fare clic sul pulsante "->".  
  
 **Oggetti tabella/vista assegnati al catalogo**  
 Elenca le tabelle e le viste attualmente assegnate al catalogo full-text.  
  
## <a name="selected-object-properties"></a>Proprietà degli oggetti selezionati  
 **Proprietà degli oggetti selezionati**  
 Visualizza le proprietà dell'oggetto selezionato nella casella di riepilogo degli oggetti assegnati al catalogo.  
  
 **Indice univoco**  
 Elenca gli indici univoci disponibili della tabella o della vista.  
  
 **La tabella è abilitato per la funzionalità full-text**  
 Selezionare questa casella di controllo per abilitare l'indice full-text nella tabella. Deselezionare la casella di controllo per disabilitare l'indice full-text.  
  
## <a name="eligible-columns-grid"></a>Griglia delle colonne idonee  
  
|||  
|-|-|  
|**Colonne disponibili**|Visualizza tutte le colonne con indice full-text. Selezionare una casella di controllo per aggiungere una colonna all'indice full-text.|  
|**Lingua per il Word Breaker**|Visualizza la lingua per il word breaker.|  
|**Colonna tipo di dati**|Viene elencato il nome della colonna nella tabella che contiene il tipo di documento della colonna elencata **colonne disponibili** se la colonna è un `varbinary(max)` o `image` colonna.|  
|**Semantica statistica**|Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica** e alla lingua selezionata non è associato alcun modello di lingua semantico, la casella di controllo **Semantica statistica** è disabilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.|  
  
## <a name="track-changes"></a>Rilevamento modifiche  
  
|||  
|-|-|  
|**Automatico**|L'indice full-text viene aggiornato automaticamente in caso di modifica, aggiunta o eliminazione dei dati nella tabella sottostante.|  
|**Manuale**|Le modifiche, le aggiunte o le eliminazioni dei dati indicizzati vengono rilevate da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando il rilevamento delle modifiche è impostato su **Manuale** , le modifiche all'indice non vengono aggiornate automaticamente. Un amministratore può invece applicare le modifiche apportate manualmente usando un [ALTER FULLTEXT INDEX... START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql) istruzione.|  
|**Non rilevare modifiche**|Quando è impostata questa opzione, le modifiche apportate ai dati indicizzati nel catalogo non vengono registrate. Un amministratore deve compilare l'indice utilizzando ALTER FULLTEXT INDEX con FULL POPULATION o INCREMENTAL POPULATION.|  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [Popolamento degli indici full-text](../relational-databases/indexes/indexes.md)  
  
  
