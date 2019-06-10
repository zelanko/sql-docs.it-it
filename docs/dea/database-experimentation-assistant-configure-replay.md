---
title: Configurare riesecuzione in Database sperimentazione Assistant per gli aggiornamenti di SQL Server
description: Configurare riesecuzione in Database sperimentazione Assistant
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: 8efef6f081395265f641197058b7920162cdde46
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794486"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>Configurare riesecuzione in Database sperimentazione Assistant

Database sperimentazione Assistant DEA () usa gli strumenti di installazione di SQL Server Distributed Replay per riprodurre una traccia acquisita su un ambiente di testing aggiornato. È consigliabile eseguire un test eseguito tramite un file di traccia di piccole dimensioni prima di eseguire una riproduzione completa per garantire una corretta riesecuzione della query.

## <a name="distributed-replay-requirements"></a>Requisiti relativi a riesecuzione distribuite

- È necessario un ulteriore 78% di spazio su disco rigido per creare file IRF sul computer del controller di riesecuzione distribuita.
- Le dimensioni di rollover della traccia ideale da usare per acquisire le tracce di produzione o di prestazioni è pari a 200 MB o 512 MB.   
- I requisiti di CPU e RAM minima per le macchine di Distributed Replay controller e client sono una CPU single core con 3,5 GB di RAM.
- Durata della riproduzione richiede circa 1.55 volte supera rispetto all'ora di acquisizione perché un controller e quattro macchine figlio vengono usate per la riproduzione della traccia di produzione.
- Se si usano la "pubblicate" versioni di produzione e i file di definizione di traccia delle prestazioni e le prestazioni traccia definizione esclude tramite filtro le tracce per un database di interesse, l'analisi mostra che il **traccia delle prestazioni** dimensioni circa 15 volte più grande di **traccia produzione** dimensioni.

## <a name="set-up-a-virtual-network-or-domain"></a>Configurare una rete virtuale o un dominio

Distributed Replay richiede di usare gli account comuni tra i computer. Questo requisito e per motivi di sicurezza, è consigliabile eseguire riesecuzione distribuita in una rete virtuale o in una rete di dominio controllati:

- Creare il controller e client macchine nell'ambiente.
- Assicurarsi che il computer controller e client può eseguire il ping reciprocamente in rete.
- Computer client di riesecuzione distribuito devono essere connessi al computer di riproduzione di destinazione che esegue SQL Server.

## <a name="set-up-the-controller-service"></a>Configurare il servizio controller

Per configurare il servizio di controller:

1. Installare il controller di riesecuzione distribuita tramite il programma di installazione di SQL Server. Se non si è eseguito il passaggio di procedura guidata di installazione di SQL Server che consente di configurare il controller di riesecuzione distribuita, è possibile configurare il controller tramite il file di configurazione. In un'installazione tipica, il file di configurazione si trova in C:\Program Files (x86) \Microsoft SQL Server\<versione\>\Tools\DReplayController\DReplayController.config.
1. Log del controller di riesecuzione distribuito si trovano in C:\Program Files (x86) \Microsoft SQL Server\<versione\>\Tools\DReplayController\Log.
1. Aprire Services. msc e passare al **SQL Server Distributed Replay Controller** servizio.
1. Pulsante destro del mouse sul servizio e quindi selezionare **proprietà**. Impostare l'account del servizio a un account che è comune per le macchine di controller e client nella rete.
1. Selezionare **OK** per chiudere la **proprietà** finestra.
1. Riavviare il **SQL Server Distributed Replay Controller** servizio da Services. msc. È anche possibile eseguire i comandi seguenti nella riga di comando per riavviare il servizio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. Per altre opzioni di configurazione, vedere [configurare Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="configure-dcom"></a>Configurare DCOM

Questa configurazione è necessaria solo nel computer del controller.

1. Aprire dcomcnfg.exe.
1. Espandere **Servizi componenti** > **computer** > **Computer** > **DCOM Config**.
1. Sotto **Config DCOM**, fare doppio clic su **DReplayController**, quindi selezionare **proprietà**.
1. Fare clic sulla scheda **Sicurezza** .
1. Sotto **autorizzazioni di esecuzione e attivazione**, selezionare **Personalizza**, quindi selezionare **Edit**.
1. Aggiungere l'utente che avvierà la riproduzione. Concedere all'utente le autorizzazioni di avvio locale e attivazione locale. Se si prevede di avviare o attivare in modalità remota, concedere all'utente le autorizzazioni di avvio remoto e attivazione remota.
1. Selezionare **OK** per salvare le modifiche e tornare alle **sicurezza** scheda.
1. Sotto **le autorizzazioni di accesso**, selezionare **Personalizza**, quindi selezionare **Edit**.
1. Aggiungere l'utente che avvierà la riproduzione. Concedere all'utente le autorizzazioni di accesso locale. Se si prevede di accedere in modalità remota il servizio controller, offrono all'utente le autorizzazioni di accesso remoto.
1. Selezionare **OK** per salvare le modifiche e tornare alle **sicurezza** scheda.
1. Selezionare **OK** per salvare le modifiche.
1. Riavviare il servizio SQL Server Distributed Replay Controller da Services. msc. È anche possibile eseguire i comandi seguenti nella riga di comando per riavviare il servizio:<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>Configurare il servizio client

Prima di configurare il servizio client, utilizzare gli strumenti di rete, ad esempio ping per verificare che il computer controller e client può comunicare.

1. Installare il client di riesecuzione distribuita tramite il programma di installazione di SQL Server.
1. Aprire Services. msc e passare al servizio di SQL Server Distributed Replay Client.
1. Pulsante destro del mouse sul servizio e quindi selezionare **proprietà**. Impostare l'account del servizio a un account che è comune a entrambi i controller e client computer della rete.
1. Selezionare **OK** per chiudere la **proprietà** finestra. Se non si è eseguito il passaggio della procedura guidata di installazione di SQL Server per configurare il client di riesecuzione distribuita, è possibile configurarlo tramite il file di configurazione. In un'installazione tipica, il file di configurazione si trova in C:\Program Files (x86) \Microsoft SQL Server\<versione\>\Tools\DReplayClient\DReplayClient.config.
1. Verificare che il file dreplayclient. config contenga il nome del computer del controller come relativo controller per la registrazione.
1.  Riavviare il servizio Client riesecuzione distribuita di SQL Server da Services. msc. È anche possibile eseguire i comandi seguenti dalla riga di comando per riavviare il servizio:<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. Log del controller di riesecuzione distribuito si trovano in C:\Program Files (x86) \Microsoft SQL Server\<versione\>\Tools\DReplayClient\Log. I log di indicano se il client può registrarsi con il controller.
1. Se la configurazione ha esito positivo, il log viene visualizzato il messaggio "registrato con il controller di < nome del controller\>".
1. Per altre opzioni di configurazione, vedere [configurare Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay).

## <a name="set-up-distributed-replay-administration-tools"></a>Configurare gli strumenti di amministrazione riesecuzione distribuita

Per verificare rapidamente se Distributed Replay funzionino correttamente nell'ambiente, è possibile usare gli strumenti di amministrazione riesecuzione distribuita. Può essere particolarmente utile in un ambiente in cui più client computer vengano registrati con un controller di test della configurazione. Si potrebbe essere necessario installare SQL Server Management Studio (SSMS) per ottenere gli strumenti di amministrazione.

1. Passare a SSMS percorso di installazione e cercare il dreplay.exe strumento Amministrazione riesecuzione distribuita e i relativi componenti dipendenti.
1. Aprire una finestra del prompt dei comandi ed eseguire `dreplay.exe status -f 1`.
1. Se tutti i passaggi precedenti hanno esito positivo, l'output della console indica che il controller può visualizzare i client in un `READY` dello stato.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Configurare il firewall per l'accesso remoto di riesecuzione distribuita

In modalità remota l'accesso a Distributed Replay richiede l'apertura di porte che sono visibili nel dominio o di una rete virtuale.

1. Aprire **Windows Firewall** con **protezione avanzata**.
1. Passare a **regole in ingresso**.
1. Creare una nuova regola firewall in entrata per programma C:\Program Files (x86) \Microsoft SQL Server\<versione\>\Tools\DReplayController\DReplayController.exe.
1. Consentire l'accesso a livello di dominio per tutte le porte per DReplayController.exe sia in grado di comunicare con il servizio di controller in modalità remota.
1. Salvare la regola.

## <a name="set-up-target-computers"></a>Configurare i computer di destinazione

Due repliche devono essere eseguiti una A o B test o un esperimento. Due istanze separate di installazioni di SQL Server, potrebbe essere necessario per uno scenario di migrazione. 

È anche possibile installare le due versioni di istanze di SQL Server nello stesso computer. Uno svantaggio consiste nell'assicurarsi che le istanze sono completamente isolate l'una volta una riproduzione in corso.

Per ogni riesecuzione, è necessario eseguire i passaggi seguenti:

1. Ripristinare il backup del database.
1. Specificare le autorizzazioni per l'utente dell'account del servizio client di accedere al database nell'istanza di SQL Server. Sono necessarie autorizzazioni per le query da eseguire nell'istanza di SQL Server.
1. Avviare la riproduzione.

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come riprodurre una traccia acquisita in un ambiente di testing aggiornato, vedere [riproduzione traccia](database-experimentation-assistant-replay-trace.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
