---
title: Proprietà colonna (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bb076297af4e666513a0c5b86d6783b7c245c00
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757614"
---
# <a name="column-properties-ssas-tabular"></a>Column Properties (SSAS Tabular)
  In questo argomento vengono descritte le proprietà delle colonne dei modelli tabulari.  
  
 Sezioni dell'argomento:  
  
-   [Proprietà delle colonne](#bkmk_properties)  
  
-   [Per configurare le impostazioni delle proprietà di colonna](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Proprietà delle colonne  
 **Standard**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Nome colonna**||Nome della colonna come archiviato nel modello e come visualizzato nell'elenco dei campi di uno strumento client di creazione report.|  
|**Formato dati**|Determinato automaticamente durante l'importazione.|Viene specificato il formato di visualizzazione da utilizzare per i dati in questa colonna. Dopo aver impostato un formato dati, è possibile impostare proprietà specifiche per ogni formato. Ad esempio, se si sceglie il formato **Valuta** , è possibile impostare il numero di posizioni decimali visibili e scegliere il separatore delle migliaia e il simbolo di valuta. Per questa proprietà sono disponibili le opzioni seguenti:<br /><br /> **Generale**<br /><br /> **Decimal Number**<br /><br /> **Numero intero**<br /><br /> **Currency**<br /><br /> **Percentuale**<br /><br /> **Notazione scientifica**<br /><br /> Se nei valori della colonna sono incluse immagini, vedere **Immagine rappresentativa**.|  
|**Tipo di dati**|Determinato automaticamente durante l'importazione.|Viene specificato il tipo di dati per tutti i valori nella colonna.|  
|**Descrizione**||Descrizione del testo della colonna.<br /><br /> In determinati client di creazione di report, se un utente finale posiziona il cursore su questa colonna nell'elenco di campi, la descrizione viene visualizzata come descrizione comando.|  
|**Hidden**|False|Viene specificato se la colonna è nascosta dalla visualizzazione negli elenchi dei campi dello strumento client di creazione report.<br /><br /> Impostare questa proprietà su **True** per nascondere questa colonna nella visualizzazione. Ad esempio, colonne contenenti identificatori o chiavi non sono in genere utili all'utente finale.<br /><br /> Se si nasconde una colonna dalla visualizzazione nello strumento client di creazione report, il campo non viene eliminato nei dati del modello. Tale campo è comunque visibile se viene creata una query sul contenuto del modello. Una colonna nascosta può ancora essere utilizzata per il raggruppamento o l'ordinamento.<br /><br /> La proprietà **Nascosta** non fornisce alcuna forma di sicurezza dei dati. Per proteggere i dati, utilizzare filtri di riga nei ruoli. Per altre informazioni, vedere [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).|  
|**Ordina per colonna**||Viene specificata un'altra colonna per ordinare i valori in questa colonna. Tra le due colonne deve esistere una relazione.<br /><br /> Questo valore deve essere il nome di una colonna esistente. Non è possibile specificare una formula o una misura.|  
  
 **Proprietà report**  
  
 Per informazioni dettagliate sull'impostazione delle proprietà del comportamento tabella [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], vedere [Configurare le proprietà Comportamento tabella per i report Power View &#40;SSAS tabulare&#41;](power-view-configure-table-behavior-properties-for-reports.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|Immagine predefinita|False|Specifica quale colonna fornisce un'immagine per rappresentare i dati della riga, ad esempio un ID foto in un record dipendente.|  
|Etichetta predefinita|False|Specifica quale colonna fornisce un nome visualizzato per rappresentare i dati della riga, ad esempio il nome del dipendente in un record dipendente.|  
|URL immagine/categoria di dati (SP1)|False|Specifica il valore in questa colonna come collegamento ipertestuale a un'immagine su un server. Ad esempio: http://localhost/images/image1.jpg.|  
|Mantieni righe univoche|False|Specifica quali colonne forniscono valori che devono essere considerati come univoci anche se duplicati, ad esempio nome e cognome del dipendente, nei casi in cui due o più dipendenti abbiano lo stesso nome.|  
|Identificatore di riga|False|Specifica una colonna che contiene solo valori univoci, consentendo l'utilizzo di tale colonna come una chiave di raggruppamento interna.|  
|Riepiloga per|Impostazione predefinita|Specifica che gli strumenti client di creazione report applicano la funzione di aggregazione SUM per i calcoli della colonna quando questa colonna viene aggiunta a un elenco Campo. Per modificare il calcolo predefinito, selezionarlo dall'elenco a discesa. Questa proprietà viene applicata solo alle colonne di tipo aggregabile.|  
|Posizione dettagli tabella|Nessun set di campi predefinito|Specifica che questa colonna o misura può essere aggiunta a un set di campi di una sola tabella per migliorare la visualizzazione della tabella in uno strumento client di creazione report.|  
  
###  <a name="bkmk_config_prop"></a> Per configurare le impostazioni delle proprietà di colonna  
  
1.  In una tabella di Progettazione modelli selezionare una colonna.  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore o fare clic sulla freccia GIÙ per selezionare un'opzione di impostazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà report Power View &#40;SSAS tabulare&#41;](properties-ssas-tabular.md)   
 [Nascondere o bloccare colonne &#40;SSAS tabulare&#41;](hide-or-freeze-columns-ssas-tabular.md)   
 [Aggiungere colonne a una tabella &#40;SSAS tabulare&#41;](add-columns-to-a-table-ssas-tabular.md)  
  
  
