---
title: Gerarchie incomplete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b3bf372682217f177d7f5a4c8b0982f1a75c4e11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740711"
---
# <a name="ragged-hierarchies"></a>Gerarchie incomplete
  Una gerarchia incompleta è una gerarchia definita dall'utente contenente un numero di livelli ineguale. Sono esempi comuni un organigramma in cui un responsabile di alto livello ha sia responsabili di reparto sia non responsabili come subalterni oppure le gerarchie geografiche composte da Paese-Regione-Città, in cui alcune città non presentano un elemento padre Stato o Provincia, ad esempio Washington D.C., Città del Vaticano o Nuova Delhi.  
  
 Nella maggior parte delle gerarchie di una dimensione, ciascun livello presenta lo stesso numero di membri di livello superiore di tutti gli altri membri allo stesso livello. In una gerarchia incompleta, invece, il membro padre logico di almeno un membro non si trova nel livello immediatamente superiore rispetto al membro. Quando si verifica questa situazione, il numero di livelli di nidificazione della gerarchia varia in base ai percorsi di drill-down. In un'applicazione client, questo può rendere i percorsi di drill-down inutilmente complicati.  
  
 Le applicazioni client variano in base alla modalità con cui, tramite esse, viene gestita una gerarchia incompleta. Se nel modello in uso sono presenti gerarchie incomplete, è necessario eseguire un lavoro supplementare per ottenere il comportamento di rendering previsto.  
  
 Innanzitutto, controllare il modo in cui l'applicazione client gestisce il percorso di drill-down. Ad esempio, tramite Excel i nomi padre vengono ripetuti come segnaposto per i valori mancanti. Per visualizzare questo comportamento, creare una tabella pivot utilizzando la dimensione Territorio vendita nel modello multidimensionale Adventure Works. In una tabella pivot che contiene gli attributi Gruppo, Paese e Regione per Territorio vendita, ai paesi che non presentano un valore relativo alla regione verrà assegnato un segnaposto, in questo caso una ripetizione dell'elemento padre al livello superiore (il nome del paese). Questo comportamento deriva dalla proprietà della stringa di connessione MDX Compatibility=1 che è fissa in Excel. Se il client non fornisce naturalmente i comportamenti di drill-down desiderati, è possibile impostare le proprietà nel modello, in modo da modificare almeno alcuni di questi comportamenti.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Approcci per la modifica della navigazione drill-down in una gerarchia incompleta](#bkmk_approach)  
  
-   [Impostazione della proprietà HideMemberIf per nascondere i membri in una gerarchia regolare](#bkmk_Hide)  
  
-   [Impostare la compatibilità MDX per determinare la rappresentazione dei segnaposto nelle applicazioni client](#bkmk_Mdx)  
  
##  <a name="bkmk_approach"></a> Approcci per la modifica della navigazione drill-down in una gerarchia incompleta  
 La presenza di una gerarchia incompleta diventa un problema quando dalla navigazione drill-down non vengono restituiti i valori previsti o viene percepita come difficile da utilizzare. Per risolvere i problemi di navigazione causati da gerarchie incomplete, possono essere considerate le seguenti opzioni:  
  
-   Utilizzare una gerarchia regolare ma impostare la proprietà `HideMemberIf` in ciascun livello, per specificare se un livello mancante viene visualizzato all'utente. Se si imposta la proprietà `HideMemberIf`, è necessario impostare anche la proprietà `MDXCompatibility` nella stringa di connessione, per sostituire i comportamenti di navigazione predefiniti. Le istruzioni per l'impostazione di queste proprietà sono fornite in questo argomento.  
  
-   Creare una gerarchia padre-figlio che gestisca esplicitamente i membri dei livelli. Per un'illustrazione della tecnica, vedere il post di blog [Ragged Hierarchy in SSAS](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)(Gerarchia incompleta in SSAS). Per altre informazioni nella documentazione Online, vedere [gerarchia padre-figlio](parent-child-dimension.md). L'aspetto negativo relativo alla creazione di una gerarchia padre-figlio è che si può disporre solo di una per ogni dimensione e che in genere si verifica una riduzione delle prestazioni durante il calcolo delle aggregazioni per i membri intermedi.  
  
 Se la dimensione contiene più di una gerarchia incompleta, è necessario utilizzare il primo approccio, impostando la proprietà `HideMemberIf`. Gli sviluppatori BI con esperienza pratica nella gestione di gerarchie incomplete vanno oltre, promuovendo modifiche aggiuntive nelle tabelle dati fisiche, mediante la creazione di tabelle separate per ciascun livello. Visualizzare [Martin Mason di gerarchie incomplete 1a parte di cubo finanziario SSAS (blog)](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) per informazioni dettagliate su questa tecnica.  
  
##  <a name="bkmk_Hide"></a> Impostazione della proprietà HideMemberIf per nascondere i membri in una gerarchia regolare  
 Nella tabella di una dimensione incompleta, i membri mancanti da un punto di vista logico possono essere rappresentati in diversi modi. Le celle della tabella possono contenere valori Null o stringhe vuote oppure possono contenere lo stesso valore del membro padre come segnaposto. La rappresentazione dei segnaposti è determinata dallo stato del segnaposto dei membri figlio, come determinato dalla proprietà `HideMemberIf` e dalla proprietà della stringa di connessione `MDX Compatibility` per l'applicazione client.  
  
 Per le applicazioni client che supportano la visualizzazione di gerarchie incomplete, è possibile utilizzare queste proprietà per nascondere i membri mancanti da un punto di vista logico.  
  
1.  In SSDT, fare doppio clic su una dimensione per aprirla in Progettazione dimensioni. Nella prima scheda, Struttura dimensione, vengono visualizzate le gerarchie di attributi nel riquadro Gerarchie.  
  
2.  Fare clic con il pulsante destro del mouse su un membro all'interno della gerarchia e scegliere **Proprietà**. Impostare la proprietà `HideMemberIf` su uno dei valori descritti in basso.  
  
    |Impostazione di HideMemberIf|Descrizione|  
    |--------------------------|-----------------|  
    |`Never`|I membri del livello non vengono mai nascosti. Rappresenta il valore predefinito.|  
    |**OnlyChildWithNoName**|Un membro del livello viene nascosto quando è l'unico elemento figlio del relativo padre e il nome è un valore Null o una stringa vuota.|  
    |**OnlyChildWithParentName**|Un membro del livello viene nascosto quando è l'unico elemento figlio del relativo padre e il nome corrisponde a quello del padre.|  
    |**NoName**|Un membro del livello viene nascosto quando il nome è vuoto.|  
    |**ParentName**|Un membro del livello viene nascosto quando il nome è identico a quello del padre.|  
  
##  <a name="bkmk_Mdx"></a> Impostare la compatibilità MDX per determinare la rappresentazione dei segnaposto nelle applicazioni client  
 Dopo aver impostato la proprietà `HideMemberIf` in un livello della gerarchia, è necessario impostare anche la proprietà `MDX Compatibility` nella stringa di connessione inviata dall'applicazione client. L'impostazione di `MDX Compatibility` determina se viene utilizzata la proprietà `HideMemberIf`.  
  
|Impostazione di MDX Compatibility|Descrizione|Uso|  
|-------------------------------|-----------------|-----------|  
|**1**|Viene visualizzato un valore di segnaposto.|Questo è il valore predefinito utilizzato da Excel, SSDT e SSMS. Indica al server di restituire i valori di segnaposto quando la navigazione drill-down svuota i livelli in una gerarchia incompleta. Se si fa clic sul valore di segnaposto, è possibile continuare la navigazione verso il basso per ottenere i nodi figlio (foglia).<br /><br /> Excel contiene la stringa di connessione utilizzata per connettersi ad Analysis Services e imposta sempre la proprietà `MDX Compatibility` su 1 per ciascuna nuova connessione. Questo comportamento preserva la compatibilità con le versioni precedenti.|  
|**2**|Viene nascosto un valore di segnaposto (un valore Null o un duplicato del livello padre) ma vengono visualizzati altri livelli e nodi che hanno valori pertinenti.|`MDX Compatibility`=2 viene in genere visualizzato come impostazione preferita in termini di gerarchie incomplete Un report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e alcune applicazioni client di terze parti possono mantenere questa impostazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare gerarchie definite dall'utente](user-defined-hierarchies-create.md)   
 [Gerarchie definite dall'utente](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Gerarchia padre-figlio](parent-child-dimension.md)   
 [Connection String Properties &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  
