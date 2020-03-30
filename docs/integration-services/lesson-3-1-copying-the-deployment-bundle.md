---
title: 'Passaggio 1: Copia del pacchetto di distribuzione| Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 12fd42ba8f7fa5abf7f35c14001cb1bc68f10096
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295983"
---
# <a name="lesson-3-1---copying-the-deployment-bundle"></a>Lezione 3-1 - Copia del pacchetto di distribuzione

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


In questa attività si procederà alla copia del pacchetto di distribuzione nel computer di destinazione.  
  
Il modo più semplice per copiare il pacchetto di distribuzione nel computer di destinazione consiste innanzitutto nella creazione di una condivisione pubblica in tale computer, l'esecuzione del mapping di un'unità alla condivisione pubblica e quindi la copia in quest'ultima del pacchetto di distribuzione. Se sono necessarie informazioni su come creare e configurare le cartelle pubbliche oppure il mapping delle unità, vedere la documentazione di Windows.  
  
### <a name="to-copy-the-deployment-bundle"></a>Per copiare il pacchetto di distribuzione  
  
1.  Individuare il pacchetto di distribuzione nel computer in uso.  
  
    Se si è utilizzato il percorso predefinito, il pacchetto di distribuzione si trova nella cartella Bin\Deployment all'interno della cartella Deployment Tutorial.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella Deployment e scegliere **Copia**.  
  
3.  Individuare la condivisione pubblica in cui si desidera copiare la cartella nel computer di destinazione e scegliere **Incolla**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Passaggio 2: Esecuzione dell'Installazione guidata pacchetti](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
  
  
