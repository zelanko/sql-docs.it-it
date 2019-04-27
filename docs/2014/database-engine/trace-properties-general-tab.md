---
title: Proprietà traccia (scheda Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.traceproperties.general.f1
helpviewer_keywords:
- Trace Properties dialog box
ms.assetid: 25227268-143b-477e-aac9-8268bcaf2078
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 35e9ee16ee50d5dc697e862b2777db7f0199970d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773803"
---
# <a name="trace-properties-general-tab"></a>Proprietà traccia (scheda Generale)
  Usare la scheda **Generale** della finestra di dialogo **Proprietà traccia** per visualizzare o specificare le proprietà di una traccia.  
  
## <a name="options"></a>Opzioni  
 **Nome traccia**  
 Consente di specificare il nome della traccia.  
  
 **Nome provider di traccia**  
 Visualizza il nome dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da inserire nella traccia. In questo campo viene inserito automaticamente il nome del server specificato al momento della connessione. Per modificare il nome del provider di traccia, fare clic su **Annulla** per chiudere la finestra di dialogo e avviare una nuova traccia.  
  
 **Tipo provider di traccia**  
 Visualizza il tipo di server che fornisce la traccia. Il campo **Tipo provider di traccia** viene popolato automaticamente dal file di definizione della traccia. Questo campo non può essere modificato.  
  
 **version**  
 Visualizza la versione del server che fornisce la traccia. Il campo **Versione** viene popolato automaticamente dal file di definizione della traccia. Questo campo non può essere modificato.  
  
 **Modello**  
 Consente di selezionare un modello dalla directory dei modelli. Questa directory viene popolata con i modelli predefiniti ed eventuali modelli definiti dall'utente creati per il tipo di provider di traccia corrente.  
  
 **Salva nel file**  
 Consente di acquisire i dati di traccia in un file trc. Il salvataggio dei dati di traccia risulta utile per eseguire analisi e controlli successivi.  
  
 **Dimensioni massime del file (MB)**  
 Se si sceglie di salvare i dati di traccia in un file, è necessario specificare le dimensioni massime del file di traccia. Il valore predefinito è 5 megabyte (MB). Le dimensioni massime sono limitate solo dal file system (NTFS, FAT) in cui viene salvato il file.  
  
 \<Graphic > **Salva con nome**  
 Se si è scelto di eseguire il salvataggio, è possibile fare clic su questa icona per modificare il nome del file.  
  
 **Consenti rollover dei file**  
 Selezionare questa opzione per abilitare la creazione di file aggiuntivi in cui acquisire i dati di traccia al raggiungimento delle dimensioni massime del file. Il nome di ogni nuovo file è composto dal nome del file trc originale e da un numero progressivo. Quando vengono ad esempio raggiunte le dimensioni massime del file **NewTrace.trc** , quest'ultimo viene chiuso e viene aperto un nuovo file, **NewTrace_1.trc**, seguito a sua volta da **NewTrace_2.trc**e così via. Quando si salva una traccia in un file, il rollover dei file è abilitato per impostazione predefinita.  
  
 **Dati di traccia elaborati dal server**  
 Consente di specificare che l'elaborazione dei dati di traccia deve essere eseguita dal server che esegue la traccia. Questa opzione consente di limitare l'overhead delle prestazioni causata dalla traccia. Se questa casella di controllo è selezionata nessun evento viene ignorato, anche in condizioni di sovraccarico. Se questa casella di controllo è deselezionata, l'elaborazione viene eseguita da SQL Server Profiler ed è possibile che alcuni eventi non vengano tracciati in condizioni di sovraccarico.  
  
 **Salva nella tabella**  
 Consente di memorizzare i dati di traccia in una tabella di database. Il salvataggio dei dati di traccia risulta utile per eseguire analisi e controlli successivi. Tuttavia il salvataggio dei dati di traccia in una tabella può causare un notevole overhead nel server in cui viene salvata la traccia. Se possibile, non salvare la tabella di traccia sullo stesso server tracciato.  
  
 \<Graphic > **tabella di destinazione**  
 Se si è scelto di eseguire il salvataggio dei dati della traccia in una tabella di database, è possibile fare clic su questa icona per modificare il nome della tabella.  
  
 **Numero massimo di righe (in migliaia)**  
 Consente di specificare il numero massimo di righe in cui salvare i dati. Il valore predefinito è 1000 righe.  
  
 **Data e ora di arresto della traccia**  
 Consente di impostare la data e l'ora di interruzione della traccia e la relativa chiusura.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una traccia &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
