---
title: Installare azdata con Windows Installer
titleSuffix: SQL Server big data clusters
description: Informazioni su come installare lo strumento azdata per l'installazione e [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] la gestione (anteprima) con il programma di installazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158146"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>Installare `azdata` per gestire [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con Windows Installer

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive come installare `azdata` per la versione finale candidata di 2019 per i cluster Big Data di SQL Server in Windows. Prima che fosse disponibile l'installazione di Windows, l' `azdata` installazione `pip`di richiedeva.

>Per Linux (Ubuntu), vedere [install `azdata` with Installer](./deploy-install-azdata-linux-package.md).

Al momento non sono disponibili gestori di pacchetti da installare `azdata` in altri sistemi operativi o distribuzioni. Per queste piattaforme, vedere [install `azdata` without Package Manager](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Installare `azdata` con il Microsoft Windows Installer

Per installare `azdata` in con il Microsoft Windows Installer,

1. Rimuovere `azdata` se è stato installato utilizzando `pip`. Se `azdata` è stato installato con Windows Installer, procedere al passaggio successivo.
1. Eseguire `azdata` l'installazione usando il Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Disinstalla se l'installazione precedente è stata eseguita con`pip`

Se sono installate versioni precedenti di **mssqlctl** , rimuoverle. Il seguente comando rimuove la versione CTP 3,1 di **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

Se sono installate versioni precedenti di, `azdata` è importante disinstallarlo prima di installare la versione più recente.

   Per la versione CTP 3,2, eseguire il comando seguente.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

Una volta rimossa, eseguire l' [ `azdata` installazione in Windows](#install-azdata-windows).

>[!NOTE]
>Se l'installazione precedente è stata eseguita utilizzando l'identità del servizio gestito, non sarà necessario disinstallare le versioni correnti prima di utilizzare il programma di installazione MSI.

### <a id="install-azdata-windows"></a>Installare con Windows Installer

Usare il Windows Installer per installare o aggiornare `azdata` in Windows.

[Scaricare il `azdata` Windows Installer](http://aka.ms/azdata-msi).

Quando il programma di installazione chiede se è possibile apportare modifiche al computer, `Yes`fare clic su.

### <a name="uninstall-azdata-with-windows-installer"></a>Disinstalla `azdata` con Windows Installer

Per disinstallare `azdata` con Windows Installer, seguire le istruzioni per il sistema operativo appropriato.

| Piattaforma      | Istruzioni                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | Avviare > Impostazioni > app                                |
| Windows 8     | Avviare > Pannello di controllo > programmi > disinstallare un programma |

Viene chiamato **`Azdata CLI`** il programma da disinstallare. Selezionare l'applicazione, quindi fare clic `Uninstall` sul pulsante.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui cluster di Big Data, vedere [che cosa [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]sono?](big-data-cluster-overview.md).
