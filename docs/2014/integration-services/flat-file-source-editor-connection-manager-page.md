---
title: Editor origine file flat (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43a0251b63d7a0519a2a19b6bec4c5117f0dcef0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425488"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>Editor origine file flat (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **Editor origine file flat** per selezionare la gestione connessione file flat per l'origine da utilizzare. L'origine file flat legge i dati da un file di testo. I dati possono essere in formato delimitato, a larghezza fissa o misto.  
  
 Un'origine file flat può utilizzare uno dei tipi seguenti di gestione connessione:  
  
-   Gestione connessione file flat se l'origine è un singolo file flat. Per ulteriori informazioni, vedere [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
-   Gestione connessione per più file flat se l'origine è data da più file flat e l'attività Flusso di dati si trova in un contenitore Ciclo, ad esempio il contenitore Ciclo For. In ogni ciclo del contenitore, l'origine file flat carica dati dal nome file successivo fornito dalla gestione connessione per più file. Per ulteriori informazioni, vedere [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
 Per ulteriori informazioni sull'origine file flat, vedere [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione file flat**  
 Consente di selezionare una gestione connessione esistente nell'elenco o di creare una nuova gestione connessione facendo clic su **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Editor gestione connessione file flat** .  
  
 **Mantieni i valori Null dell'origine come valori Null nel flusso di dati**  
 Consente di specificare se mantenere i valori Null durante l'estrazione dei dati. Il valore predefinito della proprietà è **false**. Quando questo valore è f`alse`, l'origine del file flat sostituisce i valori Null dai dati di origine con i valori predefiniti corretti per ogni colonna, ad esempio stringhe vuote per colonne con stringhe e zero per colonne numeriche.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor origine file flat &#40;pagina colonne&#41;](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [Editor origine file flat &#40;pagina output degli errori&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Gestione connessione file flat](connection-manager/file-connection-manager.md)  
  
  
