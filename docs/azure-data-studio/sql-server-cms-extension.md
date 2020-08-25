---
title: Estensione Server di gestione centrale di SQL Server
description: Informazioni su come installare e usare l'estensione Server di gestione centrale di SQL Server (anteprima), un'estensione per il raggruppamento di server e l'applicazione di azioni al gruppo.
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/06/2019
ms.openlocfilehash: 3024a9c61fb51063b50f8fde769e7bdbb5608fbf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766050"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>Estensione Server di gestione centrale di SQL Server (anteprima)

L'estensione Server di gestione centrale consente agli utenti di archiviare un elenco di istanze di SQL Server organizzato in uno o più gruppi. Le azioni eseguite tramite un gruppo di server di gestione centrale hanno effetto su tutti i server del gruppo.

Questa funzionalità è attualmente disponibile in versione di anteprima iniziale. Segnalare eventuali problemi e richieste di funzionalità [qui](https://github.com/microsoft/azuredatastudio/issues).

![Estensione Server di gestione centrale](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>Installare l'estensione Server di gestione centrale di SQL Server

1. Per aprire Gestione estensioni e accedere alle estensioni disponibili, selezionare l'icona delle estensioni oppure l'opzione **Estensioni** dal menu **Visualizza**.
2. Selezionare un'estensione disponibile per visualizzarne i dettagli.
1. Selezionare l'estensione desiderata (Server di gestione centrale di SQL Server) e **installarla**.

### <a name="how-do-i-start-central-management-servers"></a>Come è possibile avviare Server di gestione centrale?
 Per visualizzare Server di gestione centrale è possibile fare clic sull'icona Connessioni (CTRL/CMD + G). La prima volta che si scarica l'estensione, la vista di Server di gestione centrale viene ridotta a icona ed è possibile aprirla facendo clic su **Server di gestione centrale**.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni concettuali su Server di gestione centrale, [leggere qui](../ssms/register-servers/create-a-central-management-server-and-server-group.md).