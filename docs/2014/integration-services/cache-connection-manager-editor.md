---
title: Editor gestione connessione cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af7696c1d5194af721b6ff803736193db0285b8b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385049"
---
# <a name="cache-connection-manager-editor"></a>Editor gestione connessione cache
  La Gestione connessione cache consente di leggere un set di dati di riferimento dalla trasformazione cache o da un file di cache (.caw) e può salvare i dati in un file di cache. I dati vengono sempre archiviati in memoria.  
  
> [!NOTE]  
>  I tipi di dati BLOB (oggetto binario di grandi dimensioni), ovvero DT_TEXT, DT_NTEXT e DT_IMAGE, non sono supportati nella Gestione connessione cache. Se il set di dati di riferimento contiene un tipo di dati BLOB, il componente avrà esito negativo quando viene eseguito il pacchetto. È possibile utilizzare **Editor gestione connessione cache** per modificare i tipi di dati di colonna.  
  
 La trasformazione Ricerca esegue ricerche sul set di dati di riferimento.  
  
 La finestra di dialogo **Editor gestione connessione della cache** include le schede seguenti:  
  
-   [Scheda Generale](#generaltab)  
  
-   [Scheda colonne](#columnstab)  
  
 Per ulteriori informazioni sulla gestione connessione cache, vedere [Cache Connection Manager](connection-manager/cache-connection-manager.md).  
  
##  <a name="generaltab"></a> Scheda Generale  
 Usare la scheda **Generale** della finestra di dialogo **Editor gestione connessione della cache** per indicare se leggere la cache da un file o salvare la cache in un file.  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione cache nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Usa cache di file**  
 Indicare se utilizzare un file di cache.  
  
> [!NOTE]  
>  Il livello di protezione del pacchetto non si applica al file di cache. Se il file di cache contiene informazioni riservate, utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso al percorso o alla cartella nella quale verrà archiviato il file. È consigliabile consentire l'accesso solo a determinati account. Per altre informazioni, vedere [Accesso ai file utilizzati dai pacchetti](../../2014/integration-services/access-to-files-used-by-packages.md).  
  
 Se la gestione connessione della cache viene configurata in modo da utilizzare un file di cache, la gestione connessione eseguirà una delle seguenti azioni:  
  
-   Salvare i dati in un file quando la trasformazione Cache viene configurata in modo da scrivere i dati da un'origine dati nel flusso di dati alla gestione connessione della cache. Per ulteriori informazioni, vedere [Cache Transform](data-flow/transformations/cache-transform.md).  
  
-   Leggere i dati dal file di cache.  
  
 **Nome file**  
 Digitare il percorso e il nome file del file di cache.  
  
 **Sfoglia**  
 Individuare il file di cache.  
  
 **Aggiorna metadati**  
 Eliminare i metadati della colonna nella Gestione connessione cache e ripopolare la Gestione connessione cache con i metadati della colonna da un file di cache selezionato.  
  
##  <a name="columnstab"></a> Scheda Colonne  
 Utilizzare la scheda **Colonne** della finestra di dialogo **Editor gestione connessione cache** per configurare le proprietà di ciascuna colonna nella cache.  
  
### <a name="options"></a>Opzioni  
 **Colonna**  
 Consente di specificare il nome della colonna.  
  
 **Posizione dell'indice**  
 Consente di specificare quali colonne sono colonne dell'indice specificando la relativa posizione di ogni colonna. L'indice è un insieme di una o più colonne.  
  
 Per le colonne non dell'indice, la posizione è 0.  
  
 Per le colonne di indice, la posizione di indice è un numero sequenziale e positivo. Questo numero indica l'ordine con cui la trasformazione Ricerca confronta le righe nel set di dati di riferimento alle righe nell'origine dei dati di input. La colonna con più valori univoci deve disporre della posizione di indice più bassa.  
  
> [!NOTE]  
>  Quando la trasformazione Ricerca viene configurata per utilizzare una Gestione connessione cache, è possibile eseguire il mapping solo delle colonne di indice nel set di dati di riferimento alle colonne di input. Inoltre, è necessario eseguire il mapping di tutte le colonne di indice.  
  
 **Tipo**  
 Consente di specificare il tipo di dati della colonna.  
  
 `Length`  
 Specifica il tipo di dati della colonna. Se applicabile al tipo di dati, è possibile aggiornare `Length`.  
  
 `Precision`  
 Specifica la precisione per certi tipi di dati di colonna. La precisione è il numero di cifre in un numero. Se applicabile al tipo di dati, è possibile aggiornare `Precision`.  
  
 `Scale`  
 Specifica la scala per certi tipi di dati di colonna. La scala è il numero di cifre a destra della virgola decimale in un numero. Se applicabile al tipo di dati, è possibile aggiornare `Scale`.  
  
 `Code Page`  
 Specifica la tabella codici per il tipo di colonna. Se applicabile al tipo di dati, è possibile aggiornare `Code Page`.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca](data-flow/transformations/lookup-transformation.md)  
  
  
