---
title: Usare l'Indicizzazione guidata full-text | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextindexingwizard.selecttablecolumns.f1
- sql12.swb.fulltextindexingwizard.welcome.f1
- sql12.swb.fulltextindexingwizard.selectacatalog.f1
- sql12.swb.fulltextindexingwizard.progress.f1
- sql12.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql12.swb.fulltextindexingwizard.selectatableorview.f1
- sql12.swb.fulltextindexingwizard.selectchangetracking.f1
- sql12.swb.fulltextindexingwizard.selectanindex.f1
- sql12.swb.fulltextindexingwizard.summary.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fea70d6b1230b67b2eedcdf1c7d2e82d2324a0b3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016317"
---
# <a name="use-the-full-text-indexing-wizard"></a>Utilizzare l'Indicizzazione guidata full-text
  L'Indicizzazione guidata full-text ha lo scopo di semplificare la procedura di creazione di un indice full-text.  
  
#### <a name="to-use-the-full-text-indexing-wizard"></a>Per utilizzare l'Indicizzazione guidata full-text  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella nella quale si desidera creare un indice full-text, scegliere **Indice full-text**, quindi fare clic su **Definisci indice full-text**.  
  
     **Indice univoco**  
     Selezionare un indice dall'elenco a discesa. L'indice deve essere univoco, a colonna singola, che non ammette valori Null. Selezionare l'indice di chiave univoca più piccolo possibile per la chiave univoca full-text. Per prestazioni ottimali, utilizzare un indice cluster.  
  
     **Colonne disponibili**  
     Per includere una colonna nell'indice, selezionare la casella di controllo accanto al nome della colonna. Le colonne non idonee per l'indicizzazione full-text vengono visualizzate in grigio con le relative caselle di controllo disabilitate.  
  
     **Lingua per il Word breaker**  
     Consente di selezionare una lingua nell'elenco a discesa. La selezione effettuata verrà utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per identificare i word breaker corretti per l'indice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa i word breaker per individuare i delimitatori delle parole nei dati con indicizzazione full-text.  
  
     **Digitare una colonna**  
     Consente di selezionare il nome della colonna che contiene il tipo di documento della colonna sottoposta all'indicizzazione full-text.  
  
     La **colonna tipo** è abilitata solo se la colonna specificata nella colonna **colonne disponibili** è di tipo `varbinary(max)` o `image` .  
  
     **Semantica statistica**  
     Consente di selezionare se abilitare l'indicizzazione semantica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](semantic-search-sql-server.md).  
  
     Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica**e alla lingua selezionata non è associato alcun modello di lingua semantico, la casella di controllo **Semantica statistica** è disabilitata. Se si seleziona **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella casella combinata a discesa saranno limitate a quelle per cui è disponibile un modello di lingua semantico.  
  
2.  Selezionare le opzioni di rilevamento delle modifiche.  
  
     **Automatico**  
     Selezionare questo pulsante di opzione per aggiornare automaticamente l'indice full-text a mano a mano che le modifiche vengono apportate ai dati sottostanti.  
  
     **Manualmente**  
     Selezionare questo pulsante di opzione se non si desidera che l'indice full-text venga aggiornato automaticamente a mano a mano che le modifiche vengono apportate ai dati sottostanti. Le modifiche apportate ai dati sottostanti vengono mantenute. Tuttavia, per applicare le modifiche all'indice full-text è necessario avviare o pianificare il processo in modo manuale.  
  
     **Non rilevare modifiche**  
     Selezionare questo pulsante di opzione se non si desidera che l'indice full-text venga aggiornato con le modifiche apportate ai dati sottostanti.  
  
     **Avvia popolamento completo quando viene creato l'indice**  
     Selezionare questo pulsante di opzione per avviare il popolamento completo dopo il completamento della procedura guidata. Ciò comporterà la creazione della struttura dell'indice full-text nel catalogo e il suo popolamento con dati con indicizzazione full-text.  
  
3.  Selezionare il catalogo, il filegroup indice e l'elenco di parole non significative.  
  
     **Seleziona catalogo full-text**  
     Consente di selezionare un catalogo full-text dall'elenco. Il catalogo predefinito del database corrisponderà all'elemento selezionato per impostazione predefinita nell'elenco. Se non è disponibile alcun catalogo, l'elenco sarà disabilitato e la casella di controllo **Crea un nuovo catalogo** sarà selezionata e disabilitata.  
  
    |||  
    |-|-|  
    |**Crea un nuovo catalogo**|Selezionare questa casella di controllo per creare un nuovo catalogo full-text.|  
  
     **Nome**  
     Immettere un nome per il nuovo catalogo full-text.  
  
     **Imposta come catalogo predefinito**  
     Selezionare questa opzione per impostare il catalogo come predefinito per il database.  
  
     **Distinzione caratteri accentati/non accentati**  
     Consente di specificare se nel catalogo viene fatta distinzione tra caratteri accentati e non accentati. Se il database supporta la distinzione tra caratteri accentati e non accentati, l'opzione **Attiva** sarà selezionata per impostazione predefinita.  
  
     **Selezione filegroup indice**  
     Consente di specificare il filegroup in cui creare l'indice full-text.  
  
     Selezionare uno dei valori seguenti:  
  
    |valore|Descrizione|  
    |-----------|-----------------|  
    |**\<default>**|Se la tabella o la vista non è partizionata, selezionare questa opzione per utilizzare lo stesso filegroup della tabella o della vista sottostante. Se la tabella o vista è partizionata, viene utilizzato il filegroup primario.|  
    |**PRIMARIO**|Selezionare questa opzione per utilizzare il filegroup primario per il nuovo indice full-text.|  
    |*user-specified default filegroup*|Se è presente un elenco di parole non significative predefinito definito dall'utente, selezionarne il nome nell'elenco per utilizzare tale filegroup per il nuovo indice full-text.|  
  
     **Selezione elenco di parole non significative full-text**  
     Consente di specificare un elenco di parole non significative da utilizzare per l'indice full-text o di disabilitare l'utilizzo dell'elenco di parole non significative.  
  
     In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive le parole non significative vengono gestite nei database tramite oggetti denominati elenchi di parole non significative. Un *elenco di parole non significative* è un elenco che, quando associato a un indice full-text, viene applicato alle query full-text su tale indice. Per altre informazioni, vedere [Configurare e gestire parole non significative ed elenchi di parole non significative per la ricerca full-text](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Selezionare uno dei valori seguenti:  
  
    |valore|Descrizione|  
    |-----------|-----------------|  
    |**\<system>**|Selezionare questa opzione per utilizzare l'elenco di parole non significative di sistema nel nuovo indice full-text. Si tratta dell'impostazione predefinita.|  
    |**\<off>**|Selezionare questa opzione per disabilitare gli elenchi di parole non significative per il nuovo indice full-text.|  
    |*user-defined-stoplist-name*|Nell'elenco viene visualizzato il nome di ogni elenco di parole non significative definito dall'utente, se presente, creato nel database. Selezionare qualsiasi elenco di parole non significative definito dall'utente da utilizzare per il nuovo indice full-text.|  
  
4.  Facoltativamente, definire la pianificazione di popolamento. Le operazioni di indicizzazione avranno inizio immediatamente, a meno che non siano state pianificate per un'esecuzione futura. Le pianificazioni verranno create immediatamente, anche se l'esecuzione avverrà solo all'ora pianificata.  
  
     **Nuova pianificazione tabella**  
     Consente di definire una pianificazione di popolamento per una tabella.  
  
     **Nuova pianificazione catalogo**  
     Consente di definire una pianificazione di popolamento per un catalogo full-text.  
  
     **Modifica**  
     Consente di modificare una pianificazione.  
  
     **Elimina**  
     Consente di eliminare una pianificazione.  
  
5.  Visualizzare o controllare lo stato dell'Indicizzazione guidata full-text.  
  
     **Stop**  
     Consente di interrompere l'operazione corrente e impedire l'esecuzione di operazioni full-text successive da parte della procedura guidata nel corso della sessione.  
  
     **Report**  
     Al termine dell'esecuzione di tutte le operazioni, fare clic su questo pulsante per accedere a un report delle operazioni eseguite. È possibile visualizzare il report, stamparlo su file, copiarlo negli Appunti o inviarlo tramite posta elettronica.  
  
  
