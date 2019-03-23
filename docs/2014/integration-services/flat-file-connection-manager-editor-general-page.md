---
title: Flat File Connection Manager Editor (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8282cf7060f106798f2fa482f474bc5e364492ee
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387079"
---
# <a name="flat-file-connection-manager-editor-general-page"></a>Editor gestione connessione file flat (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor gestione connessione file flat** per selezionare un file e un formato di dati. Una connessione file flat consente a un pacchetto di connettersi a un file di testo.  
  
 Per ulteriori informazioni sull'Editor gestione connessione file flat, vedere [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Nome file**  
 Consente di digitare il percorso e il nome del file da utilizzare nella connessione file flat.  
  
 **Sfoglia**  
 Consente di individuare il nome del file da utilizzare nella connessione file flat.  
  
 **Impostazioni locali**  
 Consente di specificare le impostazioni locali specifiche di una lingua per l'ordinamento e i formati di data e ora.  
  
 **Unicode**  
 Indica se utilizzare il formato Unicode. Se si utilizza il formato Unicode, non è possibile specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Consente di indicare se il file utilizza il tipo di formattazione delimitato, a larghezza fissa o non allineato a destra.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate dai delimitatori specificati nella pagina **Colonne** .|  
|A larghezza fissa|Le colonne hanno una larghezza fissa.|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima. L'ultima colonna è delimitata dal delimitatore di riga.|  
  
 **Qualificatore di testo**  
 Consente di specificare il qualificatore di testo da utilizzare. Ad esempio, è possibile specificare che i campi di testo siano racchiusi tra virgolette.  
  
> [!NOTE]  
>  Dopo aver selezionato un qualificatore di testo non è possibile selezionare di nuovo l'opzione **Nessuno** . Digitare **Nessuno** per deselezionare il qualificatore di testo.  
  
 **Delimitatore riga di intestazione**  
 Consente di selezionare il delimitatore per la riga di intestazione nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|La riga di intestazione è delimitata dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|La riga di intestazione è delimitata da un carattere di ritorno a capo.|  
|**{LF}**|La riga di intestazione è delimitata da un carattere di avanzamento riga.|  
|**Punto e virgola {;}**|La riga di intestazione è delimitata da un carattere punto e virgola.|  
|**Due punti {:}**|La riga di intestazione è delimitata da un carattere due punti.|  
|**Virgola {,}**|La riga di intestazione è delimitata da una virgola.|  
|**Tabulazione {t}**|La riga di intestazione è delimitata da un carattere di tabulazione.|  
|**Barra verticale {&#124;}**|La riga di intestazione è delimitata da una barra verticale.|  
  
 **Righe di intestazione da ignorare**  
 Consente di specificare il numero di eventuali righe di intestazione o righe di dati iniziali da ignorare.  
  
 **Nomi di colonne nella prima riga di dati**  
 Consente di indicare se prevedere o fornire nomi di colonne nella prima riga di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  
