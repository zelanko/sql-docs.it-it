---
title: Installare i componenti R e Python senza accesso a Internet
description: Installazione offline dei componenti R e Python per il Machine Learning in un'istanza di SQL Server isolata dietro un firewall di rete.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bd1db578d6f1b4900f559c51521d807d7e1ec271
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594354"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>Installare i componenti R e Python per il Machine Learning in SQL Server senza accesso a Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Per impostazione predefinita, i programmi di installazione si connettono ai siti di download Microsoft per ottenere i componenti necessari e aggiornati per il Machine Learning in SQL Server. Se i vincoli del firewall impediscono al programma di installazione di raggiungere questi siti, è possibile usare un dispositivo connesso a Internet per scaricare i file, trasferirli in un server offline e quindi eseguire il programma di installazione.

I componenti per l'analisi nel database comprendono l'istanza del motore di database e componenti aggiuntivi per l'integrazione di R e Python, a seconda della versione di SQL Server. 

+ SQL Server 2019 include R, Python e Java
+ SQL Server 2017 include R e Python
+ SQL Server 2016 supporta solo R

In un server isolato, le funzionalità per il Machine Learning e quelle specifiche dei linguaggi R/Python vengono aggiunte tramite file CAB. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-offline-install"></a>Installazione offline per SQL Server 2019

Per installare SQL Server Machine Learning Services (R e Python) in un server isolato, iniziare scaricando la versione iniziale di SQL Server e i file CAB corrispondenti per il supporto di R e Python. Anche se si prevede di aggiornare immediatamente il server per usare l'aggiornamento cumulativo più recente, è necessario installare prima una versione iniziale.

> [!Note]
> SQL Server 2019 non ha Service Pack. La versione iniziale è l'unica versione di base. La manutenzione viene effettuata tramite aggiornamenti cumulativi.

### <a name="1---download-2019-cabs"></a>1 - Scaricare i file CAB 2019

In un computer che dispone di una connessione Internet, scaricare i file CAB che forniscono le funzionalità di R e Python per la versione iniziale e il supporto di installazione per SQL Server 2019.

Versione  |Collegamento di download  |
---------|---------------|
Microsoft R Open        | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686) |
Microsoft R Server      | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792) |
Microsoft Python Open   | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |
Microsoft Python Server | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685) |

> [!NOTE]
> La funzionalità Java è inclusa nel supporto di installazione di SQL Server e non necessita di un file CAB separato.

###  <a name="2---get-sql-server-2019-installation-media"></a>2- Scaricare il supporto di installazione di SQL Server 2019

1. In un computer che dispone di una connessione Internet, scaricare il [programma di installazione di SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Fare doppio clic sul programma di installazione e scegliere il tipo di installazione che consente di **scaricare il supporto**. Con questa opzione, il programma di installazione crea un file locale, con estensione iso o cab, che contiene il supporto di installazione.

   ![Scegliere il tipo di installazione che consente di scaricare il supporto](media/2019offline-download-tile.png "Scaricare il supporto di installazione")

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
## <a name="sql-server-2017-offline-install"></a>Installazione offline per SQL Server 2017

Per installare SQL Server Machine Learning Services (R e Python) in un server isolato, iniziare scaricando la versione iniziale di SQL Server e i file CAB corrispondenti per il supporto di R e Python. Anche se si prevede di aggiornare immediatamente il server per usare l'aggiornamento cumulativo più recente, è necessario installare prima una versione iniziale.

> [!Note]
> SQL Server 2017 non ha Service Pack. La versione iniziale di SQL Server è l'unica versione di base da usare. La manutenzione viene effettuata tramite aggiornamenti cumulativi. 

### <a name="1---download-2017-cabs"></a>1 - Scaricare i file CAB 2017

In un computer che dispone di una connessione Internet, scaricare i file CAB che forniscono le funzionalità di R e Python per la versione iniziale e il supporto di installazione per SQL Server 2017. 

Versione  |Collegamento di download  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2- Scaricare il supporto di installazione di SQL Server 2017

1. In un computer che dispone di una connessione Internet, scaricare il [programma di installazione di SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads). 

2. Fare doppio clic sul programma di installazione e scegliere il tipo di installazione che consente di **scaricare il supporto**. Con questa opzione, il programma di installazione crea un file locale, con estensione iso o cab, che contiene il supporto di installazione.

   ![Scegliere il tipo di installazione che consente di scaricare il supporto](media/offline-download-tile.png "Scaricare il supporto di installazione")

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="sql-server-2016-offline-install"></a>Installazione offline per SQL Server 2016

La funzionalità di analisi nel database di SQL Server 2016 supporta solo il linguaggio R, con soli due file CAB, rispettivamente per i pacchetti del prodotto e per la distribuzione Microsoft di R open source. Per iniziare, installare una delle versioni seguenti: RTM, SP 1 o SP 2. Al termine dell'installazione di base, come passaggio successivo è possibile applicare gli aggiornamenti cumulativi.

In un computer che dispone di una connessione Internet, scaricare i file CAB usati dal programma di installazione per installare in SQL Server 2016 la funzionalità di analisi nel database. 

### <a name="1---download-2016-cabs"></a>1 - Scaricare i file CAB 2016

Versione  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317) |

### <a name="2---get-sql-server-2016-installation-media"></a>2- Scaricare il supporto di installazione di SQL Server 2016

È possibile installare SQL Server 2016 RTM, SP 1 o SP 2 come versione di base nel computer di destinazione. Ognuna di queste versioni può accettare un aggiornamento cumulativo.

Per ottenere un file con estensione iso contenente il supporto di installazione è possibile usare [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/). Eseguire l'accesso e quindi usare il collegamento per i **download** per trovare la versione di SQL Server 2016 da installare. Il download è disponibile sotto forma di file con estensione iso, che è possibile copiare nel computer di destinazione per un'installazione offline.

::: moniker-end

## <a name="transfer-files"></a>Trasferire i file

Nel computer di destinazione copiare il supporto di installazione di SQL Server (con estensione iso o cab) e i file CAB della funzionalità di analisi nel database. Inserire i file CAB e il file del supporto di installazione nella stessa cartella del computer di destinazione, ad esempio la cartella %TEMP% dell'utente del programma di installazione.

La cartella %TEMP% è obbligatoria per i file CAB di Python. Per R, è possibile usare %TEMP% oppure impostare il parametro `myrcachedirectory` sul percorso del file CAB.

## <a name="run-setup"></a>Esecuzione del programma di installazione

Quando si esegue il programma di installazione di SQL Server in un computer che non è connesso a Internet, nella procedura guidata viene aggiunta una pagina **Installazione offline** per consentire di specificare il percorso dei file CAB copiati nel passaggio precedente.

1. Per iniziare l'installazione, fare doppio clic sul file con estensione iso o cab per accedere al supporto di installazione. Verrà visualizzato il file **setup.exe**.

2. Fare clic con il pulsante destro del mouse su **setup.exe** e scegliere Esegui come amministratore.

3. Quando l'installazione guidata visualizza la pagina relativa alle licenze per i componenti R o Python open source, fare clic su **Accetta**. Accettando le condizioni di licenza si può proseguire con il passaggio successivo.

4. Quando viene visualizzata la pagina **Installazione offline**, in **Percorso di installazione** specificare la cartella contenente i file CAB copiati in precedenza.

5. Continuare a seguire le istruzioni visualizzate per completare l'installazione.

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>Applicare gli aggiornamenti cumulativi

È consigliabile applicare l'aggiornamento cumulativo più recente sia al motore di database sia ai componenti di Machine Learning. Gli aggiornamenti cumulativi vengono installati tramite il programma di installazione. 

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
1. Iniziare con un'istanza di base. È possibile applicare gli aggiornamenti cumulativi solo alle installazioni esistenti della versione iniziale di SQL Server.

2. In un dispositivo connesso a Internet passare all'elenco degli aggiornamenti cumulativi per la versione di SQL Server in uso:

   + Aggiornamenti di SQL Server 2019 *(per la versione 2019 non sono ancora disponibili aggiornamenti)*
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
1. Iniziare con un'istanza di base. È possibile applicare gli aggiornamenti cumulativi solo alle installazioni esistenti della versione iniziale di SQL Server.

2. In un dispositivo connesso a Internet passare all'elenco degli aggiornamenti cumulativi per la versione di SQL Server in uso:

   + [Aggiornamenti di SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Iniziare con un'istanza di base. È possibile applicare gli aggiornamenti cumulativi solo alle installazioni esistenti della versione iniziale di SQL Server 2016 oppure di SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. In un dispositivo connesso a Internet passare all'elenco degli aggiornamenti cumulativi per la versione di SQL Server in uso:

   + [Aggiornamenti di SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)
::: moniker-end

3. Selezionare l'aggiornamento cumulativo più recente per scaricare il file eseguibile.

4. Scaricare i file CAB corrispondenti per R e Python. Per i collegamenti di download, vedere [Download dei file CAB per gli aggiornamenti cumulativi nelle istanze per l'analisi nel database di SQL Server](sql-ml-cab-downloads.md).

5. Trasferire tutti i file, eseguibili e CAB, nella stessa cartella del computer offline.

6. Eseguire il programma di installazione. Accettare le condizioni di licenza e nella pagina Selezione funzionalità esaminare le funzionalità per le quali vengono applicati gli aggiornamenti cumulativi. Dovrebbero essere visualizzate tutte le funzionalità installate per l'istanza corrente, incluse quelle di Machine Learning.

   ![Selezionare le funzionalità dall'albero delle funzionalità](media/cumulative-update-feature-selection.png "elenco di funzionalità")

5. Continuare con la procedura guidata, accettando le condizioni di licenza per le distribuzioni R e Python. Durante l'installazione viene chiesto di scegliere il percorso della cartella contenente i file CAB aggiornati.

## <a name="set-environment-variables"></a>Impostare le variabili di ambiente

Per integrare solo le funzionalità di R, è necessario impostare la variabile di ambiente **MKL_CBWR** per avere la certezza di [ottenere un output coerente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) dai calcoli di Intel Math Kernel Library (MKL).

1. Nel Pannello di controllo fare clic su **Sistema e sicurezza** > **Sistema** > **Impostazioni di sistema avanzate** > **Variabili d'ambiente**.

2. Creare una nuova variabile dell'utente o di sistema. 

   + Impostare `MKL_CBWR` come nome della variabile
   + Impostare `AUTO` come valore della variabile

Per questo passaggio è necessario riavviare il server. Se si intende abilitare l'esecuzione di script, è possibile sospendere il riavvio fino a quando non sono state completate tutte le operazioni di configurazione.

## <a name="post-install-configuration"></a>Configurazione successiva all'installazione

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Al termine dell'installazione, riavviare il servizio e quindi configurare il server per abilitare l'esecuzione di script:

+ [Abilitare l'esecuzione di script esterni](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)

Un'installazione offline iniziale di SQL Server Machine Learning Services richiede la stessa configurazione di un'installazione online:

+ [Verificare l'installazione](sql-machine-learning-services-windows-install.md#verify-installation)
+ [Configurazione aggiuntiva in base alle esigenze](sql-machine-learning-services-windows-install.md#additional-configuration)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Al termine dell'installazione, riavviare il servizio e quindi configurare il server per abilitare l'esecuzione di script:

+ [Abilitare l'esecuzione di script esterni](sql-r-services-windows-install.md#bkmk_enableFeature)

Un'installazione iniziale offline di SQL Server R Services richiede la stessa configurazione di un'installazione online:

+ [Verificare l'installazione](sql-r-services-windows-install.md#verify-installation)
+ [Configurazione aggiuntiva in base alle esigenze](sql-r-services-windows-install.md#bkmk_FollowUp)
::: moniker-end

## <a name="next-steps"></a>Passaggi successivi

Per controllare lo stato di installazione dell'istanza e risolvere i problemi comuni, vedere [Report personalizzati per SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Per informazioni su voci di log o messaggi poco noti, vedere [Domande frequenti sull'installazione e sull'aggiornamento per Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).
