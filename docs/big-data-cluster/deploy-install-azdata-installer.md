---
title: Installare azdata con Windows Installer
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e la gestione di cluster Big Data di SQL Server con il programma di installazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 72b1caab9f457ad9ba2c21792ff4927d954cb3f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784282"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>Installare `azdata` per gestire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con Windows Installer

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Questo articolo descrive come installare `azdata` per i cluster Big Data di SQL Server 2019 in Windows. Prima che fosse disponibile l'installazione per Windows, era necessario installare `azdata` con `pip`.

>Per Linux (Ubuntu), vedere [Installare `azdata` con il programma di installazione](./deploy-install-azdata-linux-package.md).

Non sono attualmente disponibili strumenti di gestione pacchetti per installare `azdata` in altri sistemi operativi o altre distribuzioni. Per queste piattaforme, vedere [Installare `azdata` senza strumenti di gestione pacchetti](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Installare `azdata` con Microsoft Windows Installer

Per installare `azdata` con Microsoft Windows Installer:

1. Rimuovere un'eventuale installazione precedente di `azdata` eseguita tramite `pip`. Se l'installazione precedente di `azdata` è stata eseguita con Windows Installer, procedere con il passaggio successivo.
1. Installare `azdata` tramite Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Disinstallare un'eventuale installazione precedente eseguita con `pip`

Se sono installate versioni precedenti di `azdata`, è importante disinstallarle prima di installare la versione più recente.

   Per rimuovere la versione finale candidata di `azdata`, eseguire il comando seguente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

Dopo la rimozione, [installare `azdata` in Windows](#install-azdata-windows).

>[!NOTE]
>Se l'installazione precedente è stata eseguita tramite MSI, non è necessario disinstallare le versioni correnti prima di usare il programma di installazione MSI.

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>Installare con Windows Installer

Usare Windows Installer per installare o aggiornare `azdata` in Windows.

[Scaricare Windows Installer per `azdata`](https://aka.ms/azdata-msi).

Quando il programma di installazione chiede l'autorizzazione per l'esecuzione di modifiche nel computer, fare clic su `Yes`.

### <a name="uninstall-azdata-with-windows-installer"></a>Disinstallare `azdata` con Windows Installer

Per disinstallare `azdata` con Windows Installer, seguire le istruzioni per il sistema operativo appropriato.

| Piattaforma      | Istruzioni                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Start > Impostazioni > App                                |
| Windows 8     | Start > Pannello di controllo -> Programmi -> Disinstalla un programma |

Il programma da disinstallare si chiama `Azdata CLI`. Selezionare questa applicazione e quindi fare clic sul pulsante `Uninstall`.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)