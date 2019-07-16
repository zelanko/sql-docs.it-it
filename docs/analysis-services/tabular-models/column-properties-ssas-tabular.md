---
title: Proprietà delle colonne nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 95a8f86b2cf2bc3cf28a128349540183c88d7fd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163103"
---
# <a name="column-properties"></a>Proprietà delle colonne 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive le proprietà colonna del modello tabulare.  
  
> [!NOTE]
>  Alcune proprietà non supportate in tutti i livelli di compatibilità.    
  
##  <a name="bkmk_properties"></a> Proprietà delle colonne  
**Advanced**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Cartella di visualizzazione**||Una cartella singola o annidata per l'organizzazione delle colonne in un elenco di campi client dell'applicazione.|  

**Base**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Nome colonna**||Nome della colonna come archiviato nel modello e come visualizzato nell'elenco dei campi di uno strumento client di creazione report.|  
|**Formato dati**|Determinato automaticamente durante l'importazione.|Viene specificato il formato di visualizzazione da utilizzare per i dati in questa colonna. Per questa proprietà sono disponibili le opzioni seguenti:<br /><br /> **Generale**<br /><br /> **Decimal Number**<br /><br /> **Numero intero**<br /><br /> **Currency**<br /><br /> **Percentuale**<br /><br /> **Notazione scientifica**<br /><br /> Dopo aver impostato un formato dati, è possibile impostare proprietà specifiche per ogni formato. Ad esempio, se si sceglie il formato **Valuta** , è possibile impostare il numero di posizioni decimali visibili e scegliere il separatore delle migliaia e il simbolo di valuta.<br /><br /> <br /><br /> Se nei valori della colonna sono incluse immagini, vedere **Immagine rappresentativa**.|  
|**Tipo di dati**|Determinato automaticamente durante l'importazione.|Viene specificato il tipo di dati per tutti i valori nella colonna.|  
|**Descrizione**||Descrizione del testo della colonna.<br /><br /> In determinati client di creazione di report, se un utente finale posiziona il cursore su questa colonna nell'elenco di campi, la descrizione viene visualizzata come descrizione comando.|  
|**Hidden**|False|Viene specificato se la colonna è nascosta dalla visualizzazione negli elenchi dei campi dello strumento client di creazione report.<br /><br /> Impostare questa proprietà su **True** per nascondere questa colonna nella visualizzazione. Ad esempio, colonne contenenti identificatori o chiavi non sono in genere utili all'utente finale.<br /><br /> Se si nasconde una colonna dalla visualizzazione nello strumento client di creazione report, il campo non viene eliminato nei dati del modello. Tale campo è comunque visibile se viene creata una query sul contenuto del modello. Una colonna nascosta può ancora essere utilizzata per il raggruppamento o l'ordinamento.<br /><br /> La proprietà **Nascosta** non fornisce alcuna forma di sicurezza dei dati. Per proteggere i dati, utilizzare filtri di riga nei ruoli. Per altre informazioni, vedere [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md).|  
|**Ordina per colonna**||Viene specificata un'altra colonna per ordinare i valori in questa colonna. Tra le due colonne deve esistere una relazione.<br /><br /> Questo valore deve essere il nome di una colonna esistente. Non è possibile specificare una formula o una misura.|  
|**Univoco**||Può essere impostato su impone l'univocità dei valori nella colonna. Sempre true per le colonne calcolate, anche se l'univocità è false.|  

 **Varie**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Hint di codifica**|Impostazione predefinita|Specifica la codifica per ottimizzare l'elaborazione. Valore di codifica, è possibile migliorare le prestazioni delle query per le colonne numeriche in genere utilizzato nelle aggregazioni. La codifica hash è per le chiavi esterne e colonne group by (spesso valori di tabella delle dimensioni). Colonne di tipo stringa sono sempre hash con codificata.|  

 **Proprietà report**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|Immagine predefinita|False|Specifica quale colonna fornisce un'immagine per rappresentare i dati della riga, ad esempio un ID foto in un record dipendente.|  
|Etichetta predefinita|False|Specifica quale colonna fornisce un nome visualizzato per rappresentare i dati della riga, ad esempio il nome del dipendente in un record dipendente.|  
|URL immagine/categoria di dati (SP1)|False|Specifica il valore in questa colonna come collegamento ipertestuale a un'immagine su un server. Ad esempio: `http://localhost/images/image1.jpg`.|  
|Mantieni righe univoche|False|Specifica quali colonne forniscono valori che devono essere considerati come univoci anche se duplicati, ad esempio nome e cognome del dipendente, nei casi in cui due o più dipendenti abbiano lo stesso nome.|  
|Identificatore di riga|False|Specifica una colonna che contiene solo valori univoci, consentendo l'utilizzo di tale colonna come una chiave di raggruppamento interna.|  
|Riepiloga per|Impostazione predefinita|Specifica che gli strumenti client di creazione report applicano la funzione di aggregazione SUM per i calcoli della colonna quando questa colonna viene aggiunta a un elenco Campo. Per modificare il calcolo predefinito, selezionarlo dall'elenco a discesa. Questa proprietà viene applicata solo alle colonne di tipo aggregabile.|  
|Posizione dettagli tabella|Nessun set di campi predefinito|Specifica che questa colonna o misura può essere aggiunta a un set di campi di una sola tabella per migliorare la visualizzazione della tabella in uno strumento client di creazione report.|  
  
##  <a name="bkmk_config_prop"></a> Configurare le impostazioni delle proprietà delle colonne  
  
1.  In una tabella di Progettazione modelli selezionare una colonna.  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore o fare clic sulla freccia GIÙ per selezionare un'opzione di impostazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà report Power View](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [Nascondere o bloccare colonne](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [Aggiungere colonne a una tabella](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  
