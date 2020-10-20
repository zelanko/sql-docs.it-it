---
title: Distribuire il database SQL di Azure tramite Notebook
description: Questa esercitazione illustra come creare un database SQL di Azure.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060888"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Creare un database SQL di Azure usando Azure Data Studio

È possibile creare un database SQL di Azure usando Azure Data Studio tramite la Distribuzione guidata e i notebook.

## <a name="pre-requisites"></a>Prerequisiti

 - [Azure Data Studio](download-azure-data-studio.md) installato
 - Un account e una sottoscrizione di Azure attivi Se non se ne ha una, [creare un account gratuito](https://azure.microsoft.com/free/).

## <a name="use-the-deployment-wizard"></a>Usare la Distribuzione guidata

Seguire questa procedura per usare la Distribuzione guidata, che fornirà le indicazioni per definire le impostazioni necessarie tramite un'esperienza di interfaccia utente intuitiva.

Per prima cosa, trovare e selezionare il database SQL di Azure nella Distribuzione guidata.

 1. In Azure Data Studio selezionare il viewlet Connessioni nel riquadro di spostamento a sinistra.
 2. Selezionare il pulsante **...** nella parte superiore del pannello Connessioni e scegliere **Nuova distribuzione**.
 3. Nella Distribuzione guidata selezionare il riquadro **Database SQL di Azure** e selezionare la casella di controllo per accettare le condizioni.
 4. Nell'elenco a discesa Tipo di risorsa selezionare il tipo di risorsa che si vuole creare, ovvero un database, un server di database o un pool elastico. Se non si dispone di database SQL in Azure, è consigliabile iniziare creando un database.
 5. Selezionare **Crea nel portale di Azure**.

Immettere quindi tutte le impostazioni preferite per la creazione del database, del server o del pool. Per informazioni su come configurare queste impostazioni, vedere la [documentazione di SQL di Azure](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal).

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato il database, il server o il pool, è possibile [connettersi ed eseguire query](quickstart-sql-database.md) sul database in Azure Data Studio.
