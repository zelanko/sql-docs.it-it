---
title: Indicatori KPI (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
author: minewiskan
ms.author: owend
ms.openlocfilehash: cdfbc4825908f409392f7dcca67749cbe08a407c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938834"
---
# <a name="kpis-ssas-tabular"></a>Indicatori KPI (SSAS tabulare)
  In un modello tabulare un indicatore di prestazioni chiave ( *KPI* ) viene usato per misurare le prestazioni di un valore, definito da una misura di *base* , rispetto a un valore di *destinazione* , definito anch'esso da una misura o da un valore assoluto. In questo argomento vengono fornite ai creatori di modelli tabulari informazioni di base sugli indicatori KPI in un modello tabulare.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Esempio](#bkmk_example)  
  
-   [Creare e modificare indicatori KPI](#bkmk_create)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> Vantaggi  
 Nella terminologia aziendale un indicatore KPI rappresenta una misurazione quantificabile per la valutazione degli obiettivi aziendali e viene stimato con una frequenza spesso elevata. Il reparto vendite di un'organizzazione può ad esempio utilizzare un indicatore KPI per misurare il profitto lordo mensile rispetto al profitto lordo previsto. Il reparto contabilità può misurare le spese mensili rispetto ai ricavi per valutare i costi, mentre un reparto risorse umane può misurare l'avvicendamento trimestrale dei dipendenti. Ognuno di questi rappresenta un esempio di utilizzo di un indicatore KPI. I professionisti aziendali utilizzano spesso gli indicatori di prestazioni chiave raggruppati in una scorecard aziendale per ottenere un riepilogo cronologico immediato e accurato del successo aziendale o per identificare le tendenze.  
  
 Un indicatore KPI di un modello tabulare include gli elementi seguenti:  
  
 **Valore di base**  
 Un valore di base è definito da una misura che restituisce un valore. Tale valore può essere, ad esempio, un'aggregazione di vendite effettive oppure una misura calcolata, quale il profitto per un dato periodo.  
  
 **Valore di destinazione**  
 Un valore di destinazione viene definito da una misura che restituisce un valore o da un valore assoluto. Ad esempio, un valore di destinazione potrebbe essere l'importo di aumento delle vendite o dei profitti che i responsabili di un'organizzazione desiderano ottenere.  
  
 **Soglie di stato**  
 Una soglia di stato viene definita dall'intervallo tra una soglia minima e massima o da un valore fisso. La soglia di stato viene visualizzata con un diagramma per consentire agli utenti di determinare facilmente lo stato del valore di base rispetto al valore di destinazione.  
  
##  <a name="example"></a><a name="bkmk_example"></a>Esempio  
 Il responsabile vendite di Adventure Works desidera creare una tabella pivot da utilizzare per visualizzare rapidamente se i dipendenti addetti alle vendite soddisfano o meno le rispettive quote di vendite per un determinato periodo (anno). Nella tabella pivot dovranno essere visualizzati, per ogni dipendente, l'importo in dollari delle vendite effettive, l'importo in dollari della quota di vendite e un semplice grafico con l'indicazione dello stato, ovvero se la quota di vendite di ognuno è inferiore, uguale o superiore a quella definita. Desidera inoltre poter sezionare i dati per anno.  
  
 A tale scopo, il responsabile vendite integra la guida dello sviluppatore della soluzione BI dell'organizzazione per aggiungere un indicatore KPI di vendita al modello tabulare di AdventureWorks. Il responsabile vendite utilizzerà quindi [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] per connettersi al modello tabulare di Adventure Works come origine dati e creerà una tabella pivot con i campi (misure e KPI) e i filtri dei dati per analizzare se la forza vendita soddisfa o meno le rispettive quote.  
  
 Nel modello viene creata una misura nella colonna SalesAmount della tabella FactResellerSales che indica l'importo in dollari delle vendite effettive per ogni dipendente addetto alle vendite. Tale misura definirà il valore di base dell'indicatore KPI.  
  
 Viene creata la misura Sales con la formula seguente:  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 Nella colonna SalesAmountQuota della tabella FactSalesQuota è definita una quota vendite per ogni dipendente. I valori in questa colonna verranno utilizzati come misura di destinazione (valore) nell'indicatore KPI.  
  
 La misura SalesAmountQuota viene creata con la formula seguente:  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  Tra la colonna EmployeeKey nella tabella FactSalesQuota e la colonna EmployeeKey nella tabella DimEmployees esiste una relazione, che risulta necessaria per rappresentare nella tabella FactSalesQuota ogni dipendente addetto alle vendite incluso nella tabella DimEmployees.  
  
 Dopo aver creato le misure da utilizzare come valore di base e valore di destinazione dell'indicatore KPI, la misura Sales verrà estesa a un nuovo KPI vendite. Nel KPI vendite la misura di destinazione SalesAmountQuota viene definita come valore di destinazione. La soglia di stato viene definita come intervallo sotto forma di percentuale, la cui destinazione è pari al 100%, a indicare che le vendite effettive definite dalla misura Sales hanno soddisfatto l'importo della quota definito nella misura di destinazione SalesAmountQuota. Le percentuali minima e massima sono definite sulla barra di stato e viene selezionato un tipo di grafico.  
  
 Il responsabile vendite può ora creare una tabella pivot aggiungendo il valore di base, il valore di destinazione e lo stato dell'indicatore KPI al campo valori. La colonna Employees viene aggiunta al campo RowLabel e la colonna CalendarYear viene aggiunta come filtro dei dati.  
  
 Il responsabile vendite può quindi sezionare per anno l'importo delle vendite effettive, l'importo della quota di vendite e lo stato per ogni dipendente addetto alle vendite. Può inoltre analizzare le tendenze di vendita negli anni per determinare se è necessario o meno modificare la quota di vendite per un dipendente.  
  
##  <a name="create-and-edit-kpis"></a><a name="bkmk_create"></a>Creare e modificare indicatori KPI  
 Per creare gli indicatori di prestazioni chiave in Progettazione modelli, verrà utilizzata la finestra di dialogo relativa al KPI. Dal momento che gli indicatori KPI devono essere associati a una misura, un indicatore KPI viene creato estendendo una misura che restituisce un valore di base, quindi creando una misura che restituisce un valore di destinazione, oppure immettendo un valore assoluto. Dopo aver definito la misura di base (valore) e il valore di destinazione, è possibile definire i parametri della soglia di stato tra i valori di base e di destinazione. Lo stato viene visualizzato in formato grafico tramite icone, barre, grafici o colori selezionabili. I valori di base e di destinazione, nonché lo stato, possono essere aggiunti a un report o a una tabella pivot come valori che possono essere sezionati rispetto ad altri campi dati.  
  
 Per visualizzare la finestra di dialogo dell'indicatore KPI, nella griglia delle misure per una tabella fare clic con il pulsante destro del mouse su una misura che verrà utilizzata come valore di base, quindi fare clic su **Crea KPI**. Dopo che una misura è stata estesa a un indicatore KPI come valore di base, verrà visualizzata un'icona insieme al nome della misura nella griglia delle misure che identifica la misura come associata a un indicatore KPI.  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Description|  
|-----------|-----------------|  
|[Creare e gestire indicatori KPI &#40;SSAS tabulare&#41;](kpis-ssas-tabular.md)|Viene descritto come creare un indicatore KPI con una misura di base, una misura di destinazione e soglie di stato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md)   
 [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)  
  
  
