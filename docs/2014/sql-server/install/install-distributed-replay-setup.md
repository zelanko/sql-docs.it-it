---
title: Installare Riesecuzione distribuita (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1e91b1b3af5c8531800f60478a4cb31d31ac3fbc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054750"
---
# <a name="install-distributed-replay-setup"></a>Installare i componenti Riesecuzione distribuita (programma di installazione)
  Installare le funzionalità di Riesecuzione distribuita di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Quando si pianifica il percorso di installazione delle funzionalità, considerare gli aspetti seguenti:  
  
-   Lo strumento di amministrazione può essere installato nello stesso computer del controller di Riesecuzione distribuita o in computer diversi.  
  
-   In ogni ambiente di Riesecuzione distribuita può essere presente un solo controller.  
  
-   Il servizio client può essere installato al massimo in 16 computer (fisici o virtuali).  
  
-   Nel computer che esegue il controller di Riesecuzione distribuita è possibile installare una sola istanza del servizio client. Se nell'ambiente di Riesecuzione distribuita sarà presente più di un client, si sconsiglia di installare il servizio client nello stesso computer del controller, poiché tale operazione potrebbe causare la diminuzione della velocità complessiva di Riesecuzione distribuita.  
  
-   Per gli scenari di test delle prestazioni, non si consiglia di installare lo strumento di amministrazione, ovvero il servizio controller di Riesecuzione distribuita, o il servizio client nell'istanza di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'installazione di tutte queste caratteristiche nel server di destinazione deve essere limitata al test funzionale per la compatibilità dell'applicazione.  
  
-   Dopo l'installazione, prima di avviare il servizio client Riesecuzione distribuita nei client è necessario che il servizio controller, ovvero il controller di Riesecuzione distribuita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , sia in esecuzione.  
  
> [!NOTE]  
>  Per rimuovere o modificare le funzionalità di Riesecuzione distribuita, utilizzare la finestra **Programmi e funzionalità** di Windows nel **Pannello di controllo**. Selezionare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nella finestra **Disinstalla o modifica programma** , quindi fare clic su **Rimuovi** per aprire l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Nella pagina **Seleziona funzionalità** selezionare le funzionalità di Riesecuzione distribuita che si desidera rimuovere.  
  
 **Prerequisiti:**  
  
-   Verificare che i computer che si desidera utilizzare dispongano dei requisiti descritti nell'argomento [Requisiti relativi a Riesecuzione distribuita](../../tools/sql-server-profiler/replay-requirements.md).  
  
-   Prima di iniziare questa procedura, è necessario creare gli account utente di dominio in cui verranno eseguiti i servizi controller e client. È consigliabile che tali account non siano membri del gruppo Administrators di Windows. Per altre informazioni, vedere la sezione Account utente e di servizio nell'argomento [Sicurezza di Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md) .  
  
    > [!NOTE]  
    >  Se lo strumento di amministrazione, il servizio controller e il servizio client sono in esecuzione nello stesso computer è possibile utilizzare gli account utente locali.  
  
 **Percorsi di installazione:**  
  
 Presupponendo che vengano utilizzati i percorsi dei file predefiniti e un'installazione standard, la directory di base si trova in C:\Programmi\Microsoft SQL Server. In tale directory, i file binari e gli assembly vengono installati nei percorsi seguenti:  
  
-   In un sistema a 32 bit:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Strumenti  
  
     \- OPPURE -  
  
     \<Share Feature Directory>\Tools \\ (directory della funzionalità condivisa alternativa fornita dall'utente)  
  
-   In un sistema a 64 bit:  
  
     C:\Programmi \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- OPPURE -  
  
     \<Share Feature Directory (x86)>\Tools \\ (directory della funzionalità condivisa alternativa (x86) fornita dall'utente)  
  
### <a name="to-install-distributed-replay-features"></a>Per installare le funzionalità di Riesecuzione distribuita  
  
1.  Per avviare l'installazione di una qualsiasi funzionalità di Riesecuzione distribuita, avviare l'Installazione guidata di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  Nella pagina **Regole di supporto per l'installazione** sono riportati i problemi che si potrebbero verificare durante l'installazione dei file di supporto dell'installazione di SQL Server. Prima di continuare con l'installazione, è necessario correggere qualsiasi errore del supporto dell'installazione.  
  
3.  Nella pagina **Product Key** selezionare un pulsante di opzione per indicare se si intende installare una versione gratuita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o una versione di produzione del prodotto con una chiave PID. Per ulteriori informazioni, vedere [edizioni e componenti di SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
4.  Nella pagina **Condizioni di licenza** leggere il contratto di licenza, quindi selezionare la casella di controllo per accettarne le condizioni. Per migliorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è inoltre possibile abilitare l'opzione relativa all'utilizzo delle funzionalità e inviare report a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  Nella pagina **File di supporto per l'installazione** fare clic su **Installa** per installare o aggiornare i file di supporto dell'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  Nella pagina **Impostazione ruolo** selezionare **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installazione funzionalità**, quindi fare clic su **Avanti** per passare alla pagina **Selezione funzionalità** .  
  
7.  Nella pagina **Selezione funzionalità** specificare le funzionalità che si desidera installare.  
  
    -   Per installare lo strumento di amministrazione, selezionare **Strumenti di gestione - Di base**.  
  
    -   Per installare il servizio controller, selezionare **Controller di Riesecuzione distribuita**.  
  
    -   Per installare il servizio client, selezionare **Client Riesecuzione distribuita**.  
  
     **Importante**: quando si configura il controller di Riesecuzione distribuita, è possibile specificare uno o più account utente da usare per eseguire i servizi client di Riesecuzione distribuita. Di seguito viene fornito l'elenco degli account supportati:  
  
    -   Account utente di dominio  
  
    -   Account utente locale creato dall'utente  
  
    -   Amministratore  
  
    -   Account virtuale e account del servizio gestito  
  
    -   Servizi di rete, Servizi locali e Sistema  
  
     Gli account di gruppo (locale o dominio) e gli altri account predefiniti (come Everyone) non sono accettati.  
  
8.  Facoltativamente, fare clic sul pulsante con i puntini di sospensione (...) per modificare il percorso della directory delle funzionalità condivise.  
  
    1.  Nei computer a 32 bit il percorso di installazione predefinito è **C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  Nei computer a 64 bit il percorso di installazione predefinito è **C:\Programmi (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
9. Al termine dell'operazione, scegliere **Avanti**.  
  
10. Nella pagina **Regole di installazione** viene convalidata la configurazione del computer tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Una volta completato il processo di convalida, fare clic su **Avanti**.  
  
11. Nella pagina **Requisiti di spazio su disco** viene calcolato lo spazio su disco necessario per le funzionalità specificate. Tale spazio viene quindi confrontato con lo spazio su disco disponibile.  
  
12. Nella pagina **Segnalazione errori** specificare le informazioni che si desidera inviare a [!INCLUDE[msCoName](../../includes/msconame-md.md)] per contribuire a migliorare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'opzione Segnalazione errori è abilitata.  
  
13. Nella pagina **Regole di configurazione per l'installazione** Controllo configurazione sistema consentirà di eseguire uno o più set di regole per convalidare la configurazione del computer con le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificate.  
  
14. Nella pagina **Installazione del programma** fare clic su **Installa**.  
  
    > [!IMPORTANT]  
    >  Dopo aver installato i componenti Riesecuzione distribuita, è necessario creare regole del firewall nei computer controller e client e concedere a ogni computer client autorizzazioni nel server di destinazione. Per altre informazioni, vedere [Completare i passaggi successivi all'installazione](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
 Negli argomenti aggiuntivi seguenti vengono illustrati altri modi per installare Riesecuzione distribuita:  
  
-   [Installare Riesecuzione distribuita dal prompt dei comandi](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [Installare i componenti Riesecuzione distribuita tramite un file di configurazione](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Per installare qualsiasi funzionalità di Riesecuzione distribuita, è necessario disporre di autorizzazioni di amministratore. Solo un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dispone di autorizzazioni sysadmin può aggiungere gli account del servizio client al ruolo del server sysadmin del server di prova. Per alcune considerazioni relative alla sicurezza di Riesecuzione distribuita, vedere [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Requisiti relativi a Riesecuzione distribuita](../../tools/sql-server-profiler/replay-requirements.md)   
 [Opzioni della riga di comando dello strumento di amministrazione &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurare Riesecuzione distribuita](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
