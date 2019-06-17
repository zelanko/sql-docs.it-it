---
title: Flat File di destinazione Editor (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 429ba1f8a12a4bd574a8304d18311a6e6e4efc79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058702"
---
# <a name="flat-file-destination-editor-connection-manager-page"></a>Editor destinazione file flat (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione file flat** per selezionare la connessione file flat per la destinazione e specificare se eseguire la sovrascrittura o l'accodamento al file di destinazione esistente. La destinazione file flat scrive dati in un file di testo che può essere in formato delimitato, a larghezza fissa o misto, a larghezza fissa con delimitatori di riga oppure non allineato a destra.  
  
 Per ulteriori informazioni sulla destinazione file flat, vedere [Flat File Destination](data-flow/flat-file-destination.md).  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione file flat**  
 Usare la casella di riepilogo per selezionare una gestione connessione esistente oppure fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuova**  
 Consente di creare una nuova connessione utilizzando le finestre di dialogo **Formato file flat** e **Editor gestione connessione file flat** .  
  
 Oltre ai formati file flat standard di larghezza delimitata e fissa e non allineati a destra, la finestra di dialogo **Formato file flat** dispone di una quarta opzione, **Larghezza fissa con delimitatori di riga**. Questa opzione rappresenta un caso speciale del formato non allineato a destra nel quale [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] aggiunge una colonna fittizia come colonna finale dei dati. Questa colonna fittizia assicura che la colonna finale abbia una larghezza fissa.  
  
 L'opzione **Larghezza fissa con delimitatori di riga** non è disponibile in **Editor gestione connessione file flat**. Se necessario, è possibile emulare questa opzione nell'editor. Per emulare questa opzione, nella pagina **Generale** dell' **Editor gestione connessione file flat**selezionare **Non allineato a destra**in **Formato**. Quindi, nella pagina **Avanzate** dell'editor aggiungere una nuova colonna fittizia come colonna finale dei dati.  
  
 **Sovrascrivi dati nel file**  
 Consente di indicare se sovrascrivere un file esistente o accodare i dati al file.  
  
 **Intestazione**  
 Consente di digitare un blocco di testo da inserire nel file prima che i dati vengano scritti. Utilizzare questa opzione per includere informazioni aggiuntive, quali le intestazioni delle colonne.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione file flat &#40;pagina Mapping&#41;](../../2014/integration-services/flat-file-destination-editor-mappings-page.md)  
  
  
