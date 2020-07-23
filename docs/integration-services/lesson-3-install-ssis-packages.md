---
title: 'Lezione 3: Installare i pacchetti SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4db3158c378d32dd472a9845e785be95130780b6
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922169"
---
# <a name="lesson-3-install-ssis-packages"></a>Lezione 3: Installare i pacchetti SSIS

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Nella [Lezione 2: Creare il pacchetto di distribuzione in SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)sono stati compilati un'utilità di distribuzione e un pacchetto di distribuzione contenente gli elementi necessari per installare i pacchetti in un altro computer. È stato inoltre verificato l'elenco dei file inclusi nel pacchetto di distribuzione ed è stato esaminato il contenuto del file manifesto creato contestualmente all'utilità di distribuzione.  
  
In questa lezione si procederà alla copia del pacchetto di distribuzione nel computer di destinazione e quindi all'esecuzione dell'Installazione guidata pacchetti per installare i pacchetti, le rispettive dipendenze e i file ausiliari nel computer. I pacchetti verranno installati nel database **msdb** di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e gli altri elementi nel file system. Dopo aver completato l'installazione dei pacchetti, questi ultimi verranno eseguiti in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mediante l'Utilità di esecuzione pacchetti allo scopo di testare la distribuzione.  
  
**Tempo stimato per il completamento della lezione:** 30 minuti  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copia del pacchetto di distribuzione](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [Passaggio 2: Esecuzione dell'Installazione guidata pacchetti](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [Passaggio 3: Test dei pacchetti distribuiti](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Copia del pacchetto di distribuzione](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  
