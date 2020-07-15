---
title: Compilare e pubblicare un progetto
description: Eseguire la compilazione e la pubblicazione con l'estensione progetti di database di SQL Server
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 4348f117b57c9b13a70f4a6db39ab6710eafd0ef
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519190"
---
# <a name="build-and-publish-a-project"></a>Compilare e pubblicare un progetto

Il processo di compilazione nell'estensione progetti di database SQL per Azure Data Studio consente la creazione di *pacchetti di applicazione livello dati* negli ambienti Windows, macOS e Linux. Il progetto può essere distribuito in un ambiente locale o cloud con il processo di pubblicazione.

## <a name="prerequisites"></a>Prerequisiti
- Installare e configurare l'[estensione progetti di database SQL per Azure Data Studio](sql-database-project-extension.md).


## <a name="build-a-database-project"></a>Compilare un progetto di database

 Nel viewlet **Progetti** in **Explorer** fare clic con il pulsante destro del mouse sul nodo radice *.sqlproj* e selezionare **Compila**.

 Verrà visualizzato automaticamente il riquadro di output con l'output del processo di compilazione.  Una compilazione corretta si conclude con il messaggio: 

 ``` ... exited with code: 0 ```


## <a name="publish-a-database-project"></a>Pubblicare un progetto di database

Dopo la compilazione del progetto tramite il processo corrispondente, è possibile pubblicare il database in un'istanza di SQL Server. Per pubblicare un progetto di database, nel viewlet **Progetti** in **Explorer** fare clic con il pulsante destro del mouse sul nodo radice *.sqlproj* e selezionare **Pubblica**.

Nella finestra di dialogo **Pubblica database** visualizzata specificare una connessione server e il nome del database da creare.

## <a name="next-steps"></a>Passaggi successivi

- [Estensione progetti di database SQL per Azure Data Studio](sql-database-project-extension.md)
- [Applicazioni livello dati](../relational-databases/data-tier-applications/data-tier-applications.md)


