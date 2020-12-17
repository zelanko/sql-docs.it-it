---
title: Installare Azure Data CLI (azdata) con Windows Installer
titleSuffix: ''
description: Informazioni su come installare lo strumento Azure Data CLI (azdata) con il programma di installazione.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5b190c50dbbeebef94cdd15314539e5ce501160
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489641"
---
# <a name="install-azure-data-cli-azdata-with-windows-installer"></a>Installare [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)] con Windows Installer

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

Questo articolo descrive come installare `azdata` in Windows con un programma di installazione. Usare `azdata` per gestire i cluster Big Data di SQL Server o i servizi dati abilitati per Azure Arc.

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>Passaggi per installare `azdata` con Microsoft Windows Installer

Per installare `azdata` con Microsoft Windows Installer:

1. Rimuovere un'eventuale installazione precedente di `azdata` eseguita tramite `pip`. Se l'installazione precedente di `azdata` è stata eseguita con Windows Installer, procedere con il passaggio successivo.
1. Installare `azdata` tramite [Windows Installer](https://aka.ms/azdata-msi).

### <a name="uninstall-azdata-with-windows-installer"></a>Disinstallare `azdata` con Windows Installer

Per disinstallare `azdata` con Windows Installer, seguire le istruzioni per il sistema operativo appropriato.

| Piattaforma      | Istruzioni                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Start > Impostazioni > App                                |
| Windows 8     | Start > Pannello di controllo -> Programmi -> Disinstalla un programma |

Il programma da disinstallare si chiama `Azure Data CLI`. Selezionare questa applicazione e quindi fare clic sul pulsante `Uninstall`.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui cluster Big Data, vedere [Che cosa sono i [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)

Usare `azdata` con i [servizi dati con abilitazione di Azure Arc](/azure/azure-arc/data/)
