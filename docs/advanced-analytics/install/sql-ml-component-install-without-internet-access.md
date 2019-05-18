---
title: Lingua di installazione di R e Python componenti senza accesso a internet - SQL Server Machine Learning
description: Offline o disconnesso R di Machine Learning e Python il programma di installazione nell'istanza di SQL Server isolata dietro un firewall di rete.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: da9676f029bb917adf15690b6870583fb0465fc4
ms.sourcegitcommit: 622bcdaa0b21258248b259f003f38e9d6f73e05a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836219"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Installare SQL Server machine learning R e Python in computer senza accesso a internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Per impostazione predefinita, i programmi di installazione connettersi a siti di download di Microsoft per ottenere necessarie e i componenti aggiornati per machine learning in SQL Server. Se i vincoli del firewall impediscono il programma di installazione di raggiungere questi siti, è possibile usare un dispositivo connesso a internet per scaricare i file di trasferimento dei file in un server offline e quindi eseguire il programma di installazione.

Analitica nel database sono costituiti da istanza del motore di database, oltre a componenti aggiuntivi per l'integrazione di R e Python, a seconda della versione di SQL Server. 

+ SQL Server 2017 include R e Python 
+ SQL Server 2016 è solo R.

In un server di tipo isolato, machine learning e le funzionalità specifiche del linguaggio R o Python vengono aggiunti tramite i file CAB. 

## <a name="sql-server-2017-offline-install"></a>Installazione offline di SQL Server 2017

Per installare SQL Server 2017 Machine Learning Services (R e Python) su un server di tipo isolato, inizia a scaricare la versione iniziale di SQL Server e supportano i file CAB corrispondenti per R e Python. Anche se si intende aggiornare immediatamente il server per utilizzare l'aggiornamento cumulativo più recente, una versione iniziale deve essere installata per primo.

> [!Note]
> SQL Server 2017 non è service pack. È la prima versione di SQL Server da usare la versione iniziale come linea di base solo con i servizi tramite solo gli aggiornamenti cumulativi. 

### <a name="1---download-2017-cabs"></a>1 - scaricare gli autisti 2017

In un computer con una connessione internet, scaricare i file CAB che fornisce le funzionalità di R e Python per la versione iniziale e il supporto di installazione per SQL Server 2017. 

Versione  |Collegamento di download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Python di Microsoft Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2: ottenere il supporto di installazione di SQL Server 2017

1. In un computer con una connessione a internet, scaricare il [programma di installazione di SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Fare doppio clic sul programma di installazione e scegliere il **supporti scaricare** tipo di installazione. Con questa opzione, il programma di installazione crea un file con estensione ISO (o con estensione cab) locale che contiene il supporto di installazione.

   ![Scegliere il supporto di download del tipo di installazione](media/offline-download-tile.png "scaricare il supporto")

## <a name="sql-server-2016-offline-install"></a>Installazione offline di SQL Server 2016

Analitica nel database di SQL Server 2016 è solo R, con solo due file CAB di file per i pacchetti di prodotto e la distribuzione di Microsoft di R open source, rispettivamente. Iniziare installando una di queste versioni: RTM, SP 1, SP 2. Una volta che un'installazione di base è in uso, gli aggiornamenti cumulativi possono essere applicati come passaggio successivo.

In un computer con una connessione a internet, scaricare i file CAB usati dal programma di installazione per installare analitica nel database in SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1 - scaricare gli autisti 2016

Versione  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2: ottenere il supporto di installazione di SQL Server 2016

È possibile installare SQL Server 2016 RTM, Service Pack 1 o Service Pack 2 come l'installazione del primo computer di destinazione. Qualsiasi di queste versioni può accettare un aggiornamento cumulativo.

Un modo per ottenere un file con estensione ISO che contiene il supporto di installazione è attraverso [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Accedi e quindi usare il **Scarica** collegamento per trovare la versione di SQL Server 2016 da installare. Il download è sotto forma di un file con estensione ISO, che è possibile copiare nel computer di destinazione per un'installazione offline.

## <a name="transfer-files"></a>Trasferimento di file

Copiare i file di analitica nel database CAB e il supporto di installazione di SQL Server (con estensione ISO o CAB) nel computer di destinazione. Posizionare il file CAB e file di supporto di installazione nella stessa cartella nel computer di destinazione, ad esempio cartella TEMP * % dell'utente il programma di installazione.

La cartella % TEMP % è necessaria per i file CAB di Python. Per R, è possibile usare % TEMP % o impostare il parametro myrcachedirectory al percorso di file CAB.

Lo screenshot seguente mostra i file CAB di SQL Server 2017 e ISO. Download di SQL Server 2016 un aspetto diverso: nome del file minor numero di file (nessun Python) e il supporto di installazione è per il 2016.

![Elenco di file da trasferire](media/offline-file-list.png "elenco File")

## <a name="run-setup"></a>Esecuzione del programma di installazione

Quando si esegue il programma di installazione di SQL Server in un computer disconnesso da internet, il programma di installazione aggiunge un **installazione Offline** pagina alla procedura guidata, in modo che sia possibile specificare il percorso dei file CAB è stato copiato nel passaggio precedente.

1. Per iniziare l'installazione, fare doppio clic il file con estensione ISO o CAB per accedere ai supporti di installazione. Dovrebbero vedere le **setup.exe** file.

2. Fare doppio clic su **setup.exe** ed eseguire come amministratore.

3. Quando l'installazione guidata viene visualizzata la pagina relativa alla licenza per i componenti di R o Python open source, fare clic su **Accept**. L'accettazione delle condizioni di licenza consente di procedere al passaggio successivo.

4. Quando si raggiunge il **installazione Offline** nella pagina **installare percorso**, specificare la cartella contenente i file CAB è stato copiato in precedenza.

   ![Pagina della procedura guidata per la selezione della cartella cab](media/screenshot-sql-offline-cab-page.png "cartella CAB")

5. Continuare seguenti le istruzioni visualizzate per completare l'installazione.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Applicare aggiornamenti cumulativi

È consigliabile applicare l'aggiornamento cumulativo più recente per il motore di database e i componenti di apprendimento automatico. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

1. Iniziare con un'istanza della linea di base. È possibile applicare gli aggiornamenti cumulativi solo per le installazioni esistenti di SQL Server:

  + Versione iniziale di SQL Server 2017
  + Versione iniziale di SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2

2. In un dispositivo connesso a internet e passare all'elenco di aggiornamento cumulativo per la versione di SQL Server:

  + [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selezionare l'aggiornamento cumulativo più recente per scaricare il file eseguibile.

4. Ottenere i file CAB corrispondenti per R e Python. Per i collegamenti ai download, vedere [CAB download per gli aggiornamenti cumulativi in analitica nel database di SQL Server istanze](sql-ml-cab-downloads.md).

5. Trasferimento di tutti i file, file eseguibile e i file CAB, nella stessa cartella nel computer offline.

6. Eseguire il programma di installazione. Accettare le condizioni di licenza, quindi nella pagina Selezione funzionalità, esaminare le funzionalità per il quale vengono applicati aggiornamenti cumulativi. Verrà visualizzata ogni funzionalità installata per l'istanza corrente, incluse le funzionalità di machine learning.

  ![Selezionare le funzionalità dall'albero delle funzionalità](media/cumulative-update-feature-selection.png "elenco delle funzionalità")

5. Continuare la procedura guidata, accettando le condizioni di licenza per le distribuzioni R e Python. Durante l'installazione, viene chiesto di scegliere il percorso della cartella che contiene i file CAB aggiornati.

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione solo con R funzionalità, è consigliabile impostare il **MKL_CBWR** variabile di ambiente [garantire coerenti con l'output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo, fare clic su **sistema e sicurezza** > **System** > **impostazioni di sistema avanzate**  >   **Le variabili di ambiente**.

2. Creare una nuova variabile di sistema o dell'utente. 

  + Nome della variabile set a `MKL_CBWR`
  + Impostare il valore della variabile `AUTO`

Questo passaggio richiede un riavvio del server. Se sta tentando di abilitare l'esecuzione dello script, è possibile rimandare il riavvio fino al completamento del tutto il lavoro di configurazione.

## <a name="post-install-configuration"></a>Configurazione successiva all'installazione

Dopo aver terminato l'installazione, riavviare il servizio e quindi configurare il server per consentire l'esecuzione di script:

+ [Abilitare l'esecuzione di script esterni (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [Abilitare l'esecuzione di script esterni (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

Un'installazione offline iniziale di Machine Learning Services di SQL Server 2017 o SQL Server 2016 R Services richiede la stessa configurazione di un'installazione online:

+ [È possibile verificarla](sql-machine-learning-services-windows-install.md#verify-installation) (per SQL Server 2016, fare clic su [qui](sql-r-services-windows-install.md#verify-installation)).
+ [Configurazione aggiuntiva se necessario](sql-machine-learning-services-windows-install.md#additional-configuration) (per SQL Server 2016, fare clic su [qui](sql-r-services-windows-install.md#bkmk_FollowUp)).

## <a name="next-steps"></a>Passaggi successivi

Per controllare lo stato dell'installazione dell'istanza e risolvere problemi comuni, vedere [report personalizzati per SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Per informazioni su tutti i messaggi familiari o voci di log, vedere [aggiornamento e installazione domande frequenti: servizi di Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md).

