---
title: Creare una Query di Data Mining usando XMLA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: acec8d8bb72566d00593634d7d2ee27a41fd9688
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62715208"
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>Creare una query di data mining usando XMLA
  È possibile creare diverse query sugli oggetti di data mining utilizzando AMO, DMX o XML/A.  
  
 XML viene utilizzato per le comunicazioni tra il server Analysis Services e tutti i client. Pertanto, anche se generalmente è molto più facile creare query sul contenuto utilizzando DMX, è possibile scrivere query tramite le istruzioni DISCOVER e COMMAND di XML/A, tramite un client che supporta il protocollo SOAP o creando una query XML/A in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 In questo argomento viene illustrato come usare i modelli XML/A disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per creare una query sul contenuto di un modello di data mining archiviato nel server corrente.  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>Esecuzione di una query sui set di righe dello schema di data mining utilizzando XML/A  
  
#### <a name="to-open-an-xmla-template"></a>Per aprire un modello XML/A  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Fare clic sull'icona del cubo per aprire l'elenco dei modelli di Analysis Services.  
  
3.  Nell'elenco di categorie dei modelli espandere prima **XMLA**, poi **Set di righe dello schema**, quindi fare doppio clic su **Discover Schema Rowsets** (Individua set di righe dello schema) per aprire il modello nell'editor del codice appropriato.  
  
4.  Nella finestra di dialogo **Connetti a Analysis Services** completare le informazioni di connessione e quindi fare clic su **Connetti**. Verrà visualizzata una nuova finestra dell'editor di query contenente il modello **Individua set di righe dello schema** .  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>Per individuare i nomi delle colonne del set di righe dello schema MINING MODEL CONTENT  
  
1.  Con il modello **Individua set di righe dello schema** aperto, fare clic su **Esegui**.  
  
     Viene visualizzato un elenco di set di righe dello schema nel riquadro **Risultati** che contiene i nomi e le colonne di tutti i set di righe disponibili nell'istanza corrente.  
  
2.  Nel **Query** riquadro, posizionare il cursore dopo  **\<Restriction List >** e premere INVIO per aggiungere una nuova riga.  
  
3.  Posizionare il cursore sulla riga vuota e digitare  **\<SchemaName > DMSCHEMA_MINING_MODEL_CONTENT\</SchemaName >**  
  
     La sezione completa delle restrizioni visualizzata sarà simile alla seguente:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  Fare clic su **Esegui**.  
  
     Nel riquadro **Risultati** viene visualizzato un elenco dei nomi delle colonne relativo al set di righe dello schema specificato.  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>Per creare una query sul contenuto utilizzando il set di righe dello schema MINING MODEL CONTENT  
  
1.  Nel modello **Individua set di righe dello schema** modificare il tipo di richiesta sostituendo il testo nei tag del tipo di richiesta.  
  
     Sostituire questa riga:  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     con la riga seguente:  
  
     **\<RequestType>DMSCHEMA_MINING_MODEL_CONTENT\</RequestType>**  
  
2.  Modificare l'elenco delle restrizioni per specificare un modello di data mining in base al nome aggiungendo una nuova condizione all'elenco di restrizioni.  
  
3.  Nel modello posizionare il cursore dopo `<Restriction List>` e premere INVIO per aggiungere una nuova riga.  
  
4.  Posizionare il cursore sulla riga vuota e digitare **<MODEL_NAME>Nome modello personale</MODEL_NAME>**  
  
     La sezione completa delle restrizioni visualizzata sarà simile alla seguente:  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  Fare clic su **Esegui**.  
  
     Nel riquadro Risultati viene visualizzata la definizione dello schema insieme ai valori del modello specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Set di righe dello schema di data mining](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
  
