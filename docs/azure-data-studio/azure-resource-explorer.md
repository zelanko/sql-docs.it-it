---
title: Esplora le risorse di SQL di Azure con Azure Resource Explorer
titleSuffix: Azure Data Studio
description: Informazioni su come esplorare e gestire Server SQL di Azure, Database SQL di Azure e istanza gestita SQL Azure tramite Azure Resource Explorer.
ms.custom: seodec18
author: yanancai
ms.author: yanacai
manager: craigg
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: d202a305468f78cf1890533292570ebb56edff12
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030115"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>Esplorare e gestire le risorse di SQL di Azure con Azure Resource Explorer

In questo documento descrive come è possibile esplorare e gestire Server SQL di Azure, database SQL di Azure e le risorse di istanza gestita SQL di Azure tramite Azure Resource Explorer in [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

>[!NOTE]
>Esplora risorse di Azure saranno supportato in fase di anteprima di SQL Server 2019 nel mese di ottobre. Successivamente, è possibile installare l'estensione di anteprima attraverso [Gestione estensioni](extensions.md) o tramite **File** > **Installa pacchetto dal pacchetto VSIX**.


## <a name="connect-to-azure"></a>Connect to Azure

Dopo aver installato il plug-in anteprima SQL, verrà visualizzata un'icona Azure nella barra dei menu a sinistra. Fare clic sull'icona per aprire Esplora risorse di Azure. Se non viene visualizzata l'icona di Azure, fare clic con il pulsante destro della barra dei menu a sinistra e selezionare **Azure Resource Explorer**.

### <a name="add-an-azure-account"></a>Aggiungere un account di Azure

Per visualizzare le risorse SQL associate agli account Azure, è innanzitutto necessario aggiungere l'account da [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

1. Aprire **account collegati** finestra di dialogo tramite l'icona di gestione di account in basso a sinistra o tramite **accedere ad Azure...**  collegamento in Esplora risorse di Azure.

    ![Accedi ad Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. Nel **account collegati** finestra di dialogo, fare clic su **aggiungere un account**.

    ![Aggiungere un account di Azure](media/azure-resource-explorer/add-an-azure-account.png)

3. Fare clic su **copiare e aprire** per aprire il browser per l'autenticazione.

    ![Pagina di autenticazione aperta nel browser](media/azure-resource-explorer/open-authentication-in-browser.png)

4. Incollare il **codice utente** nella pagina web e fare clic su **continua** per eseguire l'autenticazione.

    ![Eseguire l'autenticazione nel browser](media/azure-resource-explorer/authenticate-in-browser.png)

5. Nelle [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] è necessario individuare usato per l'accesso nell'account di Azure in **account collegati** finestra di dialogo.

    ![Azure account connesso](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>Aggiungere gli account di Azure più

Più account di Azure sono supportati in [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]. Per aggiungere gli account di Azure più, fare clic sul pulsante nella parte superiore destra del **account collegati** finestra di dialogo e seguire i passaggi con aggiunta una sezione di account di Azure per aggiungere gli account di Azure più.

![Aggiungere account di Azure più](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Rimuovere un account di Azure

Per rimuovere un oggetto esistente registrato nell'account di Azure:

1. Aprire **account collegati** dialogo tramite l'icona di gestione di account in basso a sinistra.
2. Scegliere il **X** pulsante a destra dell'account di Azure per rimuoverlo.

    ![Rimuovere l'account di Azure](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>Sottoscrizione di filtro

Una volta effettuato l'accesso a un account Azure, tutte le sottoscrizioni associate con tale visualizzazione account di Azure in Esplora risorse di Azure. È possibile filtrare le sottoscrizioni per ogni account di Azure.

1. Scegliere il **Select Subscription** pulsante a destra dell'account di Azure.

   ![Sottoscrizione di filtro](media/azure-resource-explorer/filter-subscription.png)

2. Selezionare le caselle di controllo per le sottoscrizioni di account si vuole cercare e quindi fare clic su **OK**.

   ![Selezionare la sottoscrizione](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Esplora le risorse di SQL di Azure

Per spostarsi all'interno di una risorsa di SQL di Azure in Esplora risorse di Azure, espandere gli account Azure e tipo gruppo di risorse.

Esplora risorse di Azure supporta attualmente Server SQL di Azure, Database SQL di Azure e istanza gestita SQL di Azure.

## <a name="connect-to-azure-sql-resources"></a>Connettersi alle risorse di SQL di Azure

Esplora risorse di Azure forniscono un accesso rapido che consente di connettersi a SQL Server e database per la gestione e query. 

1. Esplorazione della risorsa SQL che si desidera connettersi con la visualizzazione struttura ad albero.
2. Fare clic con il pulsante destro la risorsa e selezionare **Connect**, è anche possibile trovare il pulsante Connetti a destra della risorsa.

   ![Connessione a risorsa di SQL di Azure](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. In aperta **Connection** finestra di dialogo immettere la password e fare clic su **Connect**.

   ![Finestra di dialogo connessione SQL](media/azure-resource-explorer/sql-connection-dialog.png)
4. Il **server** automaticamente verrà visualizzata la finestra con il nuovo SQL server/database connesso dopo la connessione ha esito positivo.

## <a name="next-steps"></a>Passaggi successivi

- [Usare [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] connettersi ed eseguire query di database SQL di Azure](quickstart-sql-database.md)
- [Usare [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] per connettersi ed eseguire query sui dati in Azure SQL Data Warehouse](quickstart-sql-dw.md)