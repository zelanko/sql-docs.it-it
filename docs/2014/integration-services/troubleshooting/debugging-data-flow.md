---
title: Debug di un flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ab514b8d9e9a312b6d91d453235d99b837f6781
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439898"
---
# <a name="debugging-data-flow"></a>Debug di un flusso di dati
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] includono funzionalità e strumenti che è possibile usare per la risoluzione dei problemi dei flussi di dati in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] Progettazione offre visualizzatori dati.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] Progettazione e le trasformazioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offrono conteggi delle righe.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] Progettazione genera report di stato in fase di runtime.  
  
## <a name="data-viewers"></a>Visualizzatori dati  
 I visualizzatori dati visualizzano i dati scambiati tra due componenti in un flusso di dati. I dati possono essere visualizzati quando vengono estratti da un'origine dei dati e immessi per la prima volta in un flusso di dati, prima e dopo l'aggiornamento da parte di una trasformazione e prima che vengano caricati nella destinazione.  
  
 Per visualizzare i dati è necessario collegare visualizzatori dati al percorso che connette i due componenti flusso di dati. La possibilità di visualizzare i dati scambiati tra due componenti flusso di dati semplifica l'identificazione di valori di dati imprevisti, consente di vedere come vengono modificati i valori delle colonne da parte di una trasformazione e di individuare i motivi per cui una trasformazione non riesce. Nel caso in cui, ad esempio, una ricerca in una tabella di riferimento abbia esito negativo, per risolvere il problema potrebbe essere necessario aggiungere una trasformazione che fornisce dati predefiniti per le colonne vuote.  
  
 Un visualizzatore consente di visualizzare i dati in una griglia. Se si utilizza una griglia, è possibile selezionare le colonne da visualizzare. I valori per le colonne selezionate verranno visualizzati in formato tabulare.  
  
 È inoltre possibile collegare più visualizzatori dati in uno stesso percorso e visualizzare gli stessi dati in formati diversi, creando ad esempio una vista grafico e una visualizzazione griglia, oppure creare visualizzatori dati diversi per colonne di dati diverse.  
  
 Quando si aggiunge un visualizzatore dati a un percorso, Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] aggiunge un'icona di visualizzatore dati all'area di progettazione della scheda **Flusso di dati** , accanto al percorso. Le trasformazioni che possono avere più output, come la trasformazione Suddivisione condizionale, possono includere un visualizzatore dati per ogni percorso.  
  
 In fase di runtime viene visualizzata la finestra **Visualizzatore dati** in cui sono disponibili le informazioni specificate dal formato del visualizzatore dati. Un visualizzatore che utilizza un formato griglia, ad esempio, visualizza i dati per le colonne selezionate, il numero delle righe di output passate al componente flusso di dati e il numero delle righe visualizzate. Le informazioni vengono visualizzate un buffer dopo l'altro e il numero delle righe contenuto in ogni buffer dipende dalla larghezza delle righe nel flusso di dati.  
  
 Nella finestra di dialogo **Visualizzatore dati** è possibile copiare i dati negli Appunti, cancellare tutti i dati dalla tabella, riconfigurare il visualizzatore dati, riprendere il flusso di dati e collegare o scollegare il visualizzatore dati.  
  
#### <a name="to-add-a-data-viewer"></a>Per aggiungere un visualizzatore dati  
  
-   [Aggiunta di un visualizzatore dati a un flusso di dati](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>Conteggi delle righe  
 Il numero delle righe passate lungo un percorso viene visualizzato nell'area di progettazione della scheda **Flusso di dati** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , accanto al percorso. Tale numero viene aggiornato periodicamente mentre i dati si spostano lungo il percorso.  
  
 Nel flusso di dati è inoltre possibile aggiungere una trasformazione Conteggio righe per l'acquisizione del conteggio di righe finale in una variabile. Per altre informazioni, vedere [Trasformazione Conteggio righe](../data-flow/transformations/row-count-transformation.md).  
  
## <a name="progress-reporting"></a>Report di stato  
 Quando si esegue un pacchetto, Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] delinea i progressi compiuti nell'area di progettazione della scheda **Flusso dati** visualizzando ogni componente del flusso dati in un colore che ne indica lo stato. Quando ogni componente, inizialmente privo di colore, comincia a eseguire le operazioni previste, assume il colore giallo e, al termine, assume il colore verde. Tramite il colore rosso viene indicato che l'esecuzione del componente non è riuscita.  
  
 Il significato dei colori è descritto nella tabella seguente.  
  
|Colore|Descrizione|  
|-----------|-----------------|  
|Nessuno|In attesa di essere chiamato dal motore flusso di dati.|  
|Giallo|È in corso una trasformazione, un'operazione di estrazione o un'operazione di caricamento dei dati.|  
|Green|L'esecuzione è stata completata.|  
|rosso|Il componente è stato eseguito con errori.|  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi agli strumenti per lo sviluppo dei pacchetti](troubleshooting-tools-for-package-development.md)  
  
  
