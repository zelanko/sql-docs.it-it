---
title: Copiare un pacchetto in SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d3d26ebc097267b736b78e83adc37eb484c41162
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917581"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Copiare un pacchetto in SQL Server Data Tools
  In questo argomento viene descritto come creare un nuovo pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tramite la copia di un pacchetto esistente e come aggiornare le proprietà `Name` e `GUID` del nuovo pacchetto.  
  
### <a name="to-copy-a-package"></a>Per copiare un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera copiare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto.  
  
3.  Verificare che il pacchetto da copiare sia selezionato in Esplora soluzioni o che la scheda attiva in Progettazione SSIS sia quella che contiene il pacchetto.  
  
4.  Scegliere **Apri** dal menu **Salva \<package name> File**.  
  
    > [!NOTE]  
    >  Il comando **Salva con nome** è disponibile nel menu **File** solo se il pacchetto è aperto in Progettazione SSIS.  
  
5.  Facoltativamente, passare a un'altra cartella.  
  
6.  Modificare il nome del file del pacchetto, ricordando di mantenere l'estensione dtsx.  
  
7.  Fare clic su **Salva**.  
  
8.  Quando richiesto specificare se aggiornare il nome dell'oggetto di pacchetto in modo che corrisponda al nome del file. Se si fa clic su **Sì**, la `Name` proprietà del pacchetto verrà aggiornata. Il nuovo pacchetto viene aggiunto al progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aperto in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. Facoltativamente, fare clic sullo sfondo della scheda **Flusso di controllo** e quindi su **Proprietà**.  
  
10. Nella Finestra Proprietà fare clic sul valore della proprietà ID e quindi nell'elenco a discesa fare clic su **\<Generate New ID>** .  
  
11. Scegliere **Salva elementi selezionati** dal menu **File** per salvare il nuovo pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Salvataggio di una copia di un pacchetto](../../2014/integration-services/save-a-copy-of-a-package.md)   
 [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)   
 [Pacchetti di Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
