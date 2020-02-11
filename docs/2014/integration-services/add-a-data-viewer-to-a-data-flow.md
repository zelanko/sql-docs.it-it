---
title: Aggiungere un visualizzatore dati a un flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data viewers [Integration Services]
- data flow [Integration Services], data viewers
- adding data viewers
ms.assetid: 5e573274-a170-4132-bfc8-a8ff3a8411e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cbd45caac75d4fac3b5fffc305a9f359193191a5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062089"
---
# <a name="add-a-data-viewer-to-a-data-flow"></a>Aggiunta di un visualizzatore dati a un flusso di dati
  In questo argomento viene descritta la procedura per l'aggiunta e la configurazione di un visualizzatore dati in un flusso di dati. In un visualizzatore dati vengono visualizzati i dati in transito tra due componenti flusso di dati, ad esempio i dati estratti da un'origine dei dati prima che vengano modificati da una trasformazione del flusso di dati.  
  
 Un percorso collega i componenti in un flusso di dati connettendo l'output di un componente all'input dell'altro.  
  
 Per poter aggiungere visualizzatori dati in un pacchetto, è necessario che il pacchetto includa un'attività Flusso di dati e almeno due componenti flusso di dati connessi tra di loro.  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>Per aggiungere un visualizzatore dati in un flusso di dati  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** se non è già visualizzata.  
  
4.  Fare clic sull'attività Flusso di dati nel cui flusso di dati si vuole aggiungere un visualizzatore dati e quindi dare clic sulla scheda **Flusso di dati** .  
  
5.  Fare clic con il pulsante destro del mouse su un percorso tra due componenti del flusso di dati e quindi scegliere **Modifica**.  
  
6.  Nella pagina **Generale** è possibile visualizzare e modificare le proprietà del percorso. Ad esempio, nell'elenco a discesa **PathAnnotation** è possibile selezionare l'annotazione visualizzata accanto al percorso.  
  
7.  Nella pagina **Metadati** è possibile visualizzare i metadati delle colonne e copiarli negli Appunti.  
  
8.  Nella pagina **Visualizzatore dati** fare clic su **Abilita visualizzatore dati**.  
  
9. Nell'area Colonne da visualizzare selezionare le colonne che si desidera visualizzare nel visualizzatore dati. Per impostazione predefinita, nell'elenco **Colonne visualizzate** sono elencate e selezionate tutte le colonne disponibili. Spostare le colonne da non usare nell'elenco **Colonne inutilizzate** selezionandole e facendo clic sulla freccia sinistra.  
  
    > [!NOTE]  
    >  I valori nella griglia che rappresentano i tipi di dati DT_DATE, DT_DBTIME2, DT_FILETIME, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET vengono visualizzati come stringhe formattate ISO 8601. Uno spazio separatore sostituisce il separatore `T`. I valori che rappresentano i tipi di dati DT_DATE e DT_FILETIME includono sette cifre per i secondi frazionari. Poiché il tipo di dati DT_FILETIME memorizza solo tre cifre dei secondi frazionari, nella griglia viene visualizzato zero per le quattro cifre rimanenti. I valori che rappresentano il tipo di dati DT_DBTIMESTAMP includono tre cifre per i secondi frazionari. Per i valori che rappresentano i tipi di dati DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, il numero di cifre dei secondi frazionari corrisponde alla scala specificata per il tipo di dati della colonna. Per altre informazioni sui formati ISO 8601, vedere [Formati di data e ora](../../2014/integration-services/date-and-time-formats.md). Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).  
  
10. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazioni di Integration Services](data-flow/transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](data-flow/integration-services-paths.md)   
 [Flusso di dati](data-flow/data-flow.md)   
 [Debug di un flusso di dati](troubleshooting/debugging-data-flow.md)  
  
  
