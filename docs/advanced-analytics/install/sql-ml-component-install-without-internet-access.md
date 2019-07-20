---
title: Installare i componenti del linguaggio R e Python senza accesso a Internet
description: Offline o disconnesso Machine Learning configurazione di R e Python in un'istanza di SQL Server isolata dietro un firewall di rete.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c68ce075c34c6475828e81a66121e21afcf2482
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345018"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Installare SQL Server machine learning R e Python in computer senza accesso a Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Per impostazione predefinita, i programmi di installazione si connettono ai siti di download Microsoft per ottenere i componenti necessari e aggiornati per Machine Learning in SQL Server. Se i vincoli del firewall impediscono al programma di installazione di raggiungere questi siti, è possibile usare un dispositivo connesso a Internet per scaricare i file, trasferire i file in un server offline e quindi eseguire il programma di installazione.

L'analisi nel database è costituita dall'istanza del motore di database, oltre a componenti aggiuntivi per l'integrazione di R e Python, a seconda della versione di SQL Server. 

+ SQL Server 2017 include R e Python 
+ SQL Server 2016 è solo R.

In un server isolato, le funzionalità di machine learning e di linguaggio R/Python vengono aggiunte tramite file CAB. 

## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 installazione offline

Per installare SQL Server 2017 Machine Learning Services (R e Python) in un server isolato, iniziare scaricando la versione iniziale di SQL Server e i file CAB corrispondenti per il supporto di R e Python. Anche se si prevede di aggiornare immediatamente il server per l'utilizzo dell'aggiornamento cumulativo più recente, è necessario installare prima una versione iniziale.

> [!Note]
> SQL Server 2017 non dispone di Service Pack. Si tratta della prima versione di SQL Server usare la versione iniziale come unica linea di base, con la manutenzione solo per gli aggiornamenti cumulativi. 

### <a name="1---download-2017-cabs"></a>1-download di 2017 CAB

In un computer che dispone di una connessione Internet, scaricare i file CAB che forniscono le funzionalità di R e Python per la versione iniziale e il supporto di installazione per SQL Server 2017. 

Versione  |Collegamento di download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python aperto     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Server Microsoft Python    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-ottenere il supporto di installazione di SQL Server 2017

1. In un computer che dispone di una connessione Internet, scaricare il [programma di installazione di SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Fare doppio clic su Setup e scegliere il tipo di installazione **Scarica supporti** . Con questa opzione, il programma di installazione crea un file con estensione ISO o CAB locale contenente i supporti di installazione.

   ![Scegliere il tipo di installazione Scarica supporto](media/offline-download-tile.png "Scarica supporti")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 installazione offline

SQL Server 2016 analisi nel database è di sola lettura, con solo due file CAB per i pacchetti di prodotti e la distribuzione Microsoft di R Open Source, rispettivamente. Per iniziare, installare una delle versioni seguenti: RTM, SP 1, SP 2. Una volta eseguita un'installazione di base, è possibile applicare gli aggiornamenti cumulativi come passaggio successivo.

In un computer che dispone di una connessione Internet, scaricare i file CAB usati dal programma di installazione per installare analisi nel database SQL Server 2016. 

### <a name="1---download-2016-cabs"></a>1-download di 2016 CAB

Versione  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-ottenere il supporto di installazione di SQL Server 2016

È possibile installare SQL Server 2016 RTM, SP 1 o SP 2 come prima installazione nel computer di destinazione. Ognuna di queste versioni può accettare un aggiornamento cumulativo.

Un modo per ottenere un file con estensione ISO contenente il supporto di installazione è tramite [Visual Studio dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Eseguire l'accesso e quindi usare il collegamento **download** per trovare la versione di SQL Server 2016 che si vuole installare. Il download è sotto forma di file con estensione ISO, che è possibile copiare nel computer di destinazione per un'installazione offline.

## <a name="transfer-files"></a>Trasferimenti di file

Copiare il supporto di installazione di SQL Server (. ISO o. cab) e i file CAB di analisi nel database nel computer di destinazione. Inserire i file CAB e il file del supporto di installazione nella stessa cartella del computer di destinazione, ad esempio la cartella% TEMP * dell'utente del programma di installazione.

Per i file CAB Python è necessaria la cartella% TEMP%. Per R, è possibile usare% TEMP% o impostare il parametro myrcachedirectory sul percorso CAB.

Lo screenshot seguente mostra SQL Server file con estensione ISO e 2017 CAB. I download di SQL Server 2016 hanno un aspetto diverso: un numero inferiore di file (non Python) e il nome del file dei supporti di installazione è 2016.

![Elenco di file da trasferire](media/offline-file-list.png "Elenco di file")

## <a name="run-setup"></a>Esecuzione del programma di installazione

Quando si esegue SQL Server installazione in un computer disconnesso da Internet, il programma di installazione aggiunge una pagina di **installazione offline** alla procedura guidata in modo che sia possibile specificare il percorso dei file CAB copiati nel passaggio precedente.

1. Per iniziare l'installazione, fare doppio clic sul file con estensione ISO o CAB per accedere ai supporti di installazione. Verrà visualizzato il file **Setup. exe** .

2. Fare clic con il pulsante destro del mouse su **Setup. exe** ed eseguire come amministratore.

3. Quando l'installazione guidata Visualizza la pagina licenze per i componenti R o Python open source, fare clic su **Accetto**. L'accettazione delle condizioni di licenza consente di procedere al passaggio successivo.

4. Quando si arriva alla pagina **installazione offline** , in **percorso di installazione**specificare la cartella contenente i file CAB copiati in precedenza.

   ![Pagina della procedura guidata per la selezione della cartella CAB](media/screenshot-sql-offline-cab-page.png "Cartella CAB")

5. Continuare a seguire le istruzioni visualizzate per completare l'installazione.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Applicare gli aggiornamenti cumulativi

Si consiglia di applicare l'aggiornamento cumulativo più recente ai componenti del motore di database e di machine learning. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

1. Iniziare con un'istanza di base. È possibile applicare aggiornamenti cumulativi solo a installazioni esistenti di SQL Server:

  + SQL Server 2017 versione iniziale
  + SQL Server 2016 versione iniziale, SQL Server 2016 SP 1 o SQL Server 2016 SP 2

2. In un dispositivo connesso a Internet, passare all'elenco degli aggiornamenti cumulativi per la versione di SQL Server:

  + [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Selezionare l'aggiornamento cumulativo più recente per scaricare il file eseguibile.

4. Ottenere i file CAB corrispondenti per R e Python. Per i collegamenti di download, vedere la pagina relativa ai [download di CAB per gli aggiornamenti cumulativi in SQL Server istanze di analisi nel database](sql-ml-cab-downloads.md).

5. Trasferire tutti i file, i file eseguibili e i file CAB nella stessa cartella del computer offline.

6. Eseguire il programma di installazione. Accettare le condizioni di licenza e nella pagina Selezione funzionalità esaminare le funzionalità per le quali vengono applicati gli aggiornamenti cumulativi. Dovrebbero essere visualizzate tutte le funzionalità installate per l'istanza corrente, incluse le funzionalità di machine learning.

  ![Selezionare le funzionalità nell'albero delle funzionalità](media/cumulative-update-feature-selection.png "elenco di funzionalità")

5. Continuare con la procedura guidata, accettando le condizioni di licenza per le distribuzioni R e Python. Durante l'installazione viene richiesto di scegliere il percorso della cartella contenente i file CAB aggiornati.

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per l'integrazione della funzionalità R, è necessario impostare la variabile di ambiente **MKL_CBWR** per [garantire l'output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel pannello di controllo fare clic su sistema **e sicurezza** > **sistema** > **Impostazioni** > di sistema avanzate**variabili di ambiente**.

2. Creare un nuovo utente o una variabile di sistema. 

  + Imposta nome variabile su`MKL_CBWR`
  + Impostare il valore della variabile su`AUTO`

Per questo passaggio è necessario riavviare il server. Se si sta per abilitare l'esecuzione di script, è possibile disattivare il riavvio fino a quando non vengono eseguite tutte le operazioni di configurazione.

## <a name="post-install-configuration"></a>Configurazione successiva all'installazione

Al termine dell'installazione, riavviare il servizio e quindi configurare il server per abilitare l'esecuzione dello script:

+ [Abilitare l'esecuzione di script esterni (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [Abilitare l'esecuzione di script esterni (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

Un'installazione offline iniziale di SQL Server 2017 Machine Learning Services o 2016 SQL Server R Services richiede la stessa configurazione di un'installazione online:

+ [Verificare l'installazione](sql-machine-learning-services-windows-install.md#verify-installation)  per SQL Server 2016, fare clic [qui](sql-r-services-windows-install.md#verify-installation).
+ [Configurazione aggiuntiva in base alle esigenze](sql-machine-learning-services-windows-install.md#additional-configuration)  per SQL Server 2016, fare clic [qui](sql-r-services-windows-install.md#bkmk_FollowUp).

## <a name="next-steps"></a>Passaggi successivi

Per verificare lo stato di installazione dell'istanza di e risolvere i problemi comuni, vedere [Custom Reports for R Services per SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Per informazioni su messaggi o voci di log non note, vedere [domande frequenti sull'installazione e sull'aggiornamento Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

