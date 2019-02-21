---
title: Configurare i repository di Linux per SQL Server 2017 e 2019 | Microsoft Docs
description: Controllare e configurare i repository del codice sorgente per 2019 di SQL Server e SQL Server 2017 in Linux. Il repository del codice sorgente riguarda la versione di SQL Server che vengono applicati durante l'installazione e aggiornamento.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 65147a78fe616f83854b155f903d346aa52d69d5
ms.sourcegitcommit: c0e1db7cd1081e94a3a526136a5e166df646c9ba
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2019
ms.locfileid: "56444236"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurare i repository per l'installazione e aggiornamento di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
Questo articolo descrive come configurare il repository corretto per gli aggiornamenti e le installazioni di SQL Server 2017 e 2019 di SQL Server in Linux. Nella parte superiore, la selezione corrente verrà **Red Hat (RHEL)**.
::: zone-end

::: zone pivot="ld2-sles"
Questo articolo descrive come configurare il repository corretto per gli aggiornamenti e le installazioni di SQL Server 2017 e 2019 di SQL Server in Linux. Nella parte superiore, la selezione corrente verrà **SLES (SUSE)**.
::: zone-end

::: zone pivot="ld2-ubuntu"
Questo articolo descrive come configurare il repository corretto per gli aggiornamenti e le installazioni di SQL Server 2017 e 2019 di SQL Server in Linux. Nella parte superiore, la selezione corrente verrà **Ubuntu**.
::: zone-end

> [!TIP]
> Anteprima di SQL Server 2019 è ora disponibile! Per provarla, consultare questo articolo per configurare la nuova **mssql-server-preview** repository. Quindi installare seguendo le istruzioni riportate nel [Guida all'installazione](sql-server-linux-setup.md).

## <a id="repositories"></a>Repository

Quando si installa SQL Server in Linux, è necessario configurare un repository di Microsoft. Questo repository viene usato per acquisire il pacchetto, motore di database **mssql-server**e i relativi pacchetti di SQL Server. Esistono attualmente tre repository principali:

| Archivio | nome | Descrizione |
|---|---|---|
| **Anteprima (2017)** | **mssql-server** | Repository di SQL Server 2017 CTP e RC (sospeso). |
| **Anteprima (2019)** | **mssql-server-preview** | Anteprima di SQL Server 2019 e repository RC. |
| **CU** | **mssql-server-2017** | Repository di SQL Server 2017 Update (Cumulativo). |
| **GDR** | **mssql-server-2017-gdr** | Repository di SQL Server 2017 GDR per gli aggiornamenti critici. |

## <a id="cuversusgdr"></a> Aggiornamento cumulativo rispetto a GDR

È importante notare che esistono due tipi principali di repository per ogni distribuzione:

- **Gli aggiornamenti cumulativi (CU)**: Il repository di aggiornamenti cumulativi (CU) contiene i pacchetti per la versione di SQL Server base e le correzioni di bug o miglioramenti dopo tale versione. Gli aggiornamenti cumulativi sono specifici di una versione di rilascio, ad esempio SQL Server 2017. Essi vengono rilasciati cadenza regolare.

- **GDR**: Il repository GDR contiene i pacchetti di base versione di SQL Server e solo per gli aggiornamenti critici e aggiornamenti della sicurezza dopo tale versione. Questi aggiornamenti vengono aggiunti anche alla versione di aggiornamento Cumulativo successiva.

Ogni versione di unità di capacità e GDR contiene il pacchetto di SQL Server completo e tutti gli aggiornamenti precedenti per il repository. L'aggiornamento da una versione GDR a una versione aggiornamento Cumulativo è supportata da modifica repository configurato per SQL Server. È anche possibile [effettuare il downgrade](sql-server-linux-setup.md#rollback) a qualsiasi versione all'interno di versione principale (ad esempio: 2017).

> [!NOTE]
> È possibile aggiornare da una versione GDR a CU rilasciare in qualsiasi momento modificando i repository. L'aggiornamento da un aggiornamento Cumulativo versione a una versione GDR non è supportata.

## <a name="configure-repositories"></a>Configurare i repository

::: zone pivot="ld2-rhel"
Usare i passaggi descritti nelle sezioni seguenti per configurare i repository in Red Hat Enterprise Server (RHEL).
::: zone-end

::: zone pivot="ld2-sles"
Usare i passaggi descritti nelle sezioni seguenti per configurare i repository in SUSE Linux Enterprise Server (SLES).
::: zone-end

::: zone pivot="ld2-ubuntu"
Usare i passaggi descritti nelle sezioni seguenti per configurare i repository in Ubuntu.
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>Controllo per i repository configurati in precedenza

<!--RHEL-->
::: zone pivot="ld2-rhel"
Prima di tutto verificare se è già stato registrato un repository di SQL Server.

1. Visualizzare i file nei **/etc/yum.repos.d** directory con il comando seguente:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Cercare un file che consente di configurare la directory di SQL Server, ad esempio **mssql-server.repo**.

3. Stampare il contenuto del file.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. Il **nome** proprietà è il repository configurato. Sarà possibile identificare la tabella nel [repository](#repositories) sezione di questo articolo.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Prima di tutto verificare se è già stato registrato un repository di SQL Server.

1. Uso **zypper info** per ottenere informazioni su tutti i repository configurata in precedenza.

   ```bash
   sudo zypper info mssql-server
   ```

2. Il **Repository** proprietà è il repository configurato. Sarà possibile identificare la tabella nel [repository](#repositories) sezione di questo articolo.

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Prima di tutto verificare se è già stato registrato un repository di SQL Server.

1. Visualizzare il contenuto del **/etc/apt/sources.list** file.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Esaminare l'URL del pacchetto mssql-server. Sarà possibile identificare la tabella nel [repository](#repositories) sezione di questo articolo.

::: zone-end

## <a name="remove-old-repository"></a>Rimuovere i vecchi repository

<!--RHEL-->
::: zone pivot="ld2-rhel"
Se necessario, rimuovere il repository precedente con il comando seguente.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Questo comando dà per scontato che il file identificato nella sezione precedente è stato denominato **mssql-server.repo**.

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Se necessario, rimuovere il repository precedente. Usare uno dei comandi seguenti in base al tipo di repository configurato in precedenza.

| Archivio | Comando da rimuovere |
|---|---|
| **Anteprima (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Anteprima (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Se necessario, rimuovere il repository precedente. Usare uno dei comandi seguenti in base al tipo di repository configurato in precedenza.

| Archivio | Comando da rimuovere |
|---|---|
| **Anteprima (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Anteprima (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>Configurare il nuovo repository

<!--RHEL-->
::: zone pivot="ld2-rhel"
Configurare il nuovo repository da usare per gli aggiornamenti e installazioni di SQL Server. Usare uno dei comandi seguenti per configurare il repository scelto dall'utente.

| Archivio | Versione | Comando |
|---|---|---|
| **Anteprima (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
Configurare il nuovo repository da usare per gli aggiornamenti e installazioni di SQL Server. Usare uno dei comandi seguenti per configurare il repository scelto dall'utente.

| Archivio | Versione | Comando |
|---|---|---|
| **Anteprima (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
Configurare il nuovo repository da usare per gli aggiornamenti e installazioni di SQL Server.

1. Importare le chiavi GPG repository pubblico.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Usare uno dei comandi seguenti per configurare il repository scelto dall'utente.

   | Archivio | Versione | Comando |
   |---|---|---|
   | **Anteprima (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Eseguire **apt-get update**.

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato il repository corretto, è possibile procedere alla [installare](sql-server-linux-setup.md#platforms) oppure [aggiornare](sql-server-linux-setup.md#upgrade) SQL Server e i relativi pacchetti dal repository di nuovo.

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> A questo punto, se si sceglie di usare la [Guida introduttiva RHEL](quickstart-install-connect-red-hat.md), tenere presente che già stato configurato il repository di destinazione. Non ripetere questo passaggio nelle esercitazioni. Ciò vale soprattutto se si configura il repository GDR, perché la Guida introduttiva viene usato il repository CU.
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> A questo punto, se si sceglie di usare la [Guida introduttiva SLES](quickstart-install-connect-suse.md), tenere presente che già stato configurato il repository di destinazione. Non ripetere questo passaggio nelle esercitazioni. Ciò vale soprattutto se si configura il repository GDR, perché la Guida introduttiva viene usato il repository CU.
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> A questo punto, se si sceglie di usare la [Guida introduttiva di Ubuntu](quickstart-install-connect-ubuntu.md), tenere presente che già stato configurato il repository di destinazione. Non ripetere questo passaggio nelle esercitazioni. Ciò vale soprattutto se si configura il repository GDR, perché la Guida introduttiva viene usato il repository CU.
::: zone-end

Per altre informazioni su come installare SQL Server 2017 in Linux, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md).
