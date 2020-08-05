---
title: Estensione SQL Server dacpac
description: Informazioni su come installare e avviare la procedura guidata dell'applicazione a livello di dati, che semplifica la distribuzione e l'estrazione dei file con estensione DACAPC, nonché l'importazione e l'esportazione di file con estensione BACPAC.
ms.custom: seodec18
ms.date: 11/04/2019
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: eeff69a65751097017383399784ea9a717f3b7e8
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522475"
---
# <a name="sql-server-dacpac-extension"></a>Estensione SQL Server dacpac

La **procedura guidata applicazione livello dati**  rappresenta un'esperienza di procedura guidata facile da usare per distribuire ed estrarre file dacpac e importare ed esportare file bacpac.


## <a name="features"></a>Funzionalità

* Distribuzione di un dacpac in un'istanza di SQL Server
* Estrazione di un'istanza di SQL Server in un dacpac
* Creazione di un database da un bacpac
* Esportazione dello schema e dei dati in un bacpac

![gif demo dell'estensione dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-demo.gif)


## <a name="why-would-i-use-the-data-tier-application-wizard"></a>Perché usare la procedura guidata applicazione livello dati?

La procedura guidata semplifica la gestione dei file dacpac e bacpac e facilita quindi lo sviluppo e la distribuzione di elementi livello dati a supporto dell'applicazione. Per altre informazioni sull'uso di applicazioni livello dati, [vedere la documentazione.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)


## <a name="install-the-extension"></a>Installare l'estensione

1. Selezionare l'icona Estensioni per visualizzare le estensioni disponibili.

    ![icona Gestione estensioni](media/extensions/extension-manager-icon.png)

2. Cercare l'estensione **dacpac di SQL Server** e selezionarla per visualizzarne i dettagli. Fare clic su **Installa** per aggiungere l'estensione.

3. Dopo l'installazione, **ricaricare** per abilitare l'estensione in Azure Data Studio (necessario solo quando si installa un'estensione per la prima volta).


## <a name="launch-the-data-tier-application-wizard"></a>Avviare la procedura guidata applicazione livello dati

Per avviare la procedura guidata, fare clic con il pulsante destro del mouse sulla cartella Database o su un database specifico in Esplora oggetti e quindi fare clic su **Data-tier Application Wizard** (Procedura guidata applicazione livello dati).

![menu di avvio dell'estensione dacpac](media/extensions/sql-server-dacpac-extension/dacpac-extension-launch.png)


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui dacpac, [vedere la documentazione.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)
Segnalare eventuali problemi e richieste di funzionalità [qui](https://github.com/microsoft/azuredatastudio/issues).