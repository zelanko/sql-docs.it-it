---
title: Riprodurre dati di traccia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 19ff5285-fb9d-4fd1-97c4-ec72c311c384
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: efb54bb64481dc29c50976cb58df813bad411f9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63149883"
---
# <a name="replay-trace-data"></a>Riproduzione di dati di traccia
  È possibile avviare una riproduzione distribuita con la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funzionalità riesecuzione distribuita dopo aver preparato i dati di traccia di input. Per altre informazioni, vedere [Preparazione dei dati di traccia di input](prepare-the-input-trace-data.md).  
  
 Usare l'opzione **replay** dello strumento di amministrazione per avviare la fase di riproduzione dell'evento della riesecuzione distribuita. Questa fase è costituita da due parti: il recapito dei dati di traccia e l'avvio e la sincronizzazione della riproduzione distribuita.  
  
 ![Riproduzione di eventi distribuita](../../database-engine/media/eventreplay.gif "Riproduzione di eventi distribuita")  
  
 È possibile riprodurre i dati di traccia in una delle due modalità di sequenza disponibili, ovvero la modalità di stress o la modalità di sincronizzazione. Il comportamento predefinito consiste nel riprodurre i dati di traccia in modalità di stress. Per altre informazioni sulla fase di riproduzione dell'evento e sulle modalità di sequenza, vedere [SQL Server Distributed Replay](sql-server-distributed-replay.md).  
  
> [!NOTE]  
>  È necessario acquisire i dati di traccia di input in una versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibile con Distributed Replay. I dati di traccia di input devono essere compatibili anche con il server di destinazione su cui si desidera riprodurre i dati di traccia. Per altre informazioni sui requisiti relativi alla versione, vedere [Requisiti relativi a Riesecuzione distribuita](distributed-replay-requirements.md).  
  
### <a name="to-replay-the-trace"></a>Per riprodurre la traccia  
  
1.  **(Facoltativo) modificare le impostazioni di configurazione**della riproduzione: se si desidera modificare le impostazioni di configurazione della riproduzione, ad esempio la modalità di sequenziazione e diversi valori di scalabilità `<ReplayOptions>` , è necessario modificare l'elemento del file `DReplay.exe.replay.config`di configurazione della riproduzione basato su XML. È possibile modificare anche l'elemento `<OutputOptions>` per specificare impostazioni di output, ad esempio se registrare o meno il conteggio delle righe. Se si modifica il file di configurazione della riproduzione, è consigliabile modificarne una copia anziché l'originale. Per modificare le impostazioni, effettuare le operazioni seguenti:  
  
    1.  Creare una copia del file di configurazione della riproduzione predefinito `DReplay.exe.replay.config`e rinominare il nuovo file. Il file di configurazione della riproduzione predefinito si trova nella cartella di installazione dello strumento di amministrazione.  
  
    2.  Modificare le impostazioni di configurazione della riproduzione nel nuovo file di configurazione.  
  
    3.  Quando si avvia la fase di riproduzione dell'evento (passaggio successivo), usare il parametro *config_file* dell'opzione **replay** per specificare il percorso del file di configurazione modificato.  
  
     Per altre informazioni sul file di configurazione della riproduzione, vedere [Configurare Distributed Replay](configure-distributed-replay.md).  
  
2.  **Avviare la fase di riproduzione dell'evento**: per avviare la riproduzione distribuita, è necessario eseguire lo strumento di amministrazione con l'opzione **Replay** . Per altre informazioni, vedere [Opzione replay &#40;strumento di amministrazione Distributed Replay&#41;](replay-option-distributed-replay-administration-tool.md).  
  
    1.  Aprire l'utilità del prompt dei comandi di Windows (`CMD.exe`) e passare al percorso di installazione dello strumento di amministrazione di Distributed Replay (`DReplay.exe`).  
  
    2.  (Facoltativo) Usare il parametro *controller* , **-m**, per specificare il controller, se il servizio controller viene eseguito in un computer diverso dallo strumento di amministrazione.  
  
    3.  Usare il parametro *controller_working_directory* , **-d**, per specificare il percorso in cui è stato salvato il file intermedio nel controller durante la fase di pre-elaborazione.  
  
    4.  (Facoltativo) Usare **-o** per acquisire l'attività di riproduzione in un file di traccia dei risultati in ciascun client.  
  
    5.  (Facoltativo) Usare il parametro *target_server* , **-s**, per specificare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui i client Riesecuzione distribuita dovranno riprodurre il carico di lavoro dei file di traccia. Questo parametro non è necessario se è stato utilizzato l'elemento `<Server>` per specificare il server di destinazione nell'elemento `<ReplayOptions>` del file di configurazione della riproduzione.  
  
    6.  Usare il parametro *clients* , **-w**, per specificare i client Riesecuzione distribuita che dovranno partecipare alla riproduzione. Elencare i nomi dei computer client, separati da virgole. Nota: gli indirizzi IP non sono consentiti.  
  
    7.  (Facoltativo) Usare il parametro *config_file* , **-c**, per specificare il percorso del file di configurazione della riproduzione. Utilizzare questo parametro per puntare al nuovo file di configurazione se è stata modificata una copia del file di configurazione della riproduzione predefinito.  
  
    8.  (Facoltativo) Usare il parametro *status_interval* , **-f**, per specificare se si vuole che lo strumento di amministrazione visualizzi messaggi di stato a una frequenza diversa da 30 secondi.  
  
     La sintassi seguente, ad esempio, avvia la fase di riproduzione nello stesso computer del servizio controller, utilizza una directory di lavoro del controller situata in `c:\WorkingDir`, acquisisce l'attività di riproduzione in ogni client partecipante, utilizza i client `client1` e `client2` per eseguire la riproduzione e ottiene le impostazioni di configurazione della riproduzione rimanenti da un file di configurazione della riproduzione modificato che si trova in `c:\modifiedreplay.config`:  
  
     `dreplay replay -d c:\WorkingDir -o -w client1,client2 -c c:\modifiedreplay.config`  
  
3.  Al termine della riproduzione distribuita, lo strumento di amministrazione restituisce informazioni di riepilogo. Se è stata specificata l'opzione **-o** , l'attività di riproduzione è stata salvata in file di traccia dei risultati in ciascun client. Per altre informazioni sui file di traccia dei risultati, vedere [Controllo dei risultati della riproduzione](review-the-replay-results.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti di Riesecuzione distribuita](distributed-replay-requirements.md)   
 [Opzioni della riga di comando dello strumento di amministrazione &#40;Riesecuzione distribuita Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurare Distributed Replay](configure-distributed-replay.md)  
  
  
