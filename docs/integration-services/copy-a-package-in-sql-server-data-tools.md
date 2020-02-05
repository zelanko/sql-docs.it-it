---
title: Copiare un pacchetto in SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b374955ea4a07cd94de88202fe02ffbb572d0a1c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293645"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Copiare un pacchetto in SQL Server Data Tools

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Questo argomento descrive come creare un nuovo pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tramite la copia di un pacchetto esistente e come aggiornare le proprietà **Name** e **GUID** del nuovo pacchetto.  
  
### <a name="to-copy-a-package"></a>Per copiare un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera copiare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto.  
  
3.  Verificare che il pacchetto da copiare sia selezionato in Esplora soluzioni o che la scheda attiva in Progettazione SSIS sia quella che contiene il pacchetto.  
  
4.  Nel menu **File** scegliere **Salva \<nome pacchetto> con nome**.  
  
    > [!NOTE]  
    >  Il comando **Salva con nome** è disponibile nel menu **File** solo se il pacchetto è aperto in Progettazione SSIS.  
  
5.  Facoltativamente, passare a un'altra cartella.  
  
6.  Modificare il nome del file del pacchetto, ricordando di mantenere l'estensione dtsx.  
  
7.  Fare clic su **Salva**.  
  
8.  Quando richiesto specificare se aggiornare il nome dell'oggetto di pacchetto in modo che corrisponda al nome del file. Se si sceglie **Sì**, la proprietà **Name** del pacchetto verrà aggiornata. Il nuovo pacchetto viene aggiunto al progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aperto in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. Facoltativamente, fare clic sullo sfondo della scheda **Flusso di controllo** e quindi su **Proprietà**.  
  
10. Nella finestra Proprietà fare clic sul valore della proprietà ID e quindi selezionare **\<Genera nuovo ID>** nell'elenco a discesa.  
  
11. Scegliere **Salva elementi selezionati** dal menu **File** per salvare il nuovo pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Salvataggio di una copia di un pacchetto](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Creare pacchetti in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Pacchetti di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md)  
  
  
