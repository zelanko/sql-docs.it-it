---
title: Proprietà catalogo full-text (pagina tabelle e viste) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.tablesviews.f1
ms.assetid: 2d45fcd2-0f0f-4167-9027-316d6696c106
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2cab8e460b2091f9b4be90f32b7e08b15b4cf60b
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000951"
---
# <a name="full-text-catalog-properties-tables-and-views-page"></a>Proprietà catalogo full-text (pagina Tabelle e viste)
  Utilizzare questa finestra di dialogo per visualizzare o modificare le tabelle e le viste assegnate al catalogo full-text.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Tutti gli oggetti tabella/vista idonei nel database**  
 Elenca le tabelle e le viste che hanno un indice univoco definito, ma che non fanno già parte del catalogo full-text. Per selezionare una tabella o una vista e assegnarla al catalogo, selezionare gli elementi nella casella di riepilogo e premere il pulsante "->".  
  
 **Oggetti tabella/vista assegnati al catalogo**  
 Elenca le tabelle e le viste attualmente assegnate al catalogo full-text.  
  
## <a name="selected-object-properties"></a>Proprietà degli oggetti selezionati  
 **Proprietà degli oggetti selezionati**  
 Visualizza le proprietà dell'oggetto selezionato nella casella di riepilogo degli oggetti assegnati al catalogo.  
  
 **Indice univoco**  
 Elenca gli indici univoci disponibili della tabella o della vista.  
  
 **Tabella abilitata per la funzionalità full-text**  
 Selezionare questa casella di controllo per abilitare l'indice full-text nella tabella. Deselezionare la casella di controllo per disabilitare l'indice full-text.  
  
## <a name="eligible-columns-grid"></a>Griglia delle colonne idonee  
  
|||  
|-|-|  
|**Colonne disponibili**|Visualizza tutte le colonne con indice full-text. Selezionare una casella di controllo per aggiungere una colonna all'indice full-text.|  
|**Lingua per il Word breaker**|Visualizza la lingua per il word breaker.|  
|**Colonna tipo di dati**|Elenca il nome della colonna nella tabella che contiene il tipo di documento della colonna elencata in **colonne disponibili** se la colonna è una `varbinary(max)` colonna o `image` .|  
|**Semantica statistica**|Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica**e alla lingua selezionata non è associato alcun modello di lingua semantico, la casella di controllo **Semantica statistica** è disabilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.|  
  
## <a name="track-changes"></a>Rilevamento modifiche  
  
|||  
|-|-|  
|**Automatic** (Automatica)|L'indice full-text viene aggiornato automaticamente in caso di modifica, aggiunta o eliminazione dei dati nella tabella sottostante.|  
|**Manuale**|Le modifiche, le aggiunte o le eliminazioni dei dati indicizzati vengono rilevate da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando il rilevamento delle modifiche è impostato su **Manuale** , le modifiche all'indice non vengono aggiornate automaticamente. Un amministratore può invece applicare manualmente le modifiche utilizzando un' [istruzione ALTER FULLTEXT index... START UPDATE POPULATION](/sql/t-sql/statements/alter-fulltext-index-transact-sql) (istruzione).|  
|**Non rilevare modifiche**|Quando è impostata questa opzione, le modifiche apportate ai dati indicizzati nel catalogo non vengono registrate. Un amministratore deve compilare l'indice utilizzando ALTER FULLTEXT INDEX con FULL POPULATION o INCREMENTAL POPULATION.|  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)   
 [Popolamento degli indici full-text](../relational-databases/indexes/indexes.md)  
  
  
