---
title: Importare un progetto di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8fb6b68cbb30e9bbf19f854cf1dd1e7e0dd19d25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768043"
---
# <a name="import-an-integration-services-project"></a>Importare un progetto di Integration Services
  Utilizzare l'**Importazione guidata progetto** di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per creare un progetto da un file di distribuzione esistente (ispac) o da un progetto distribuito nel catalogo di Integration Services. Questa caratteristica è utile soprattutto quando non si dispone della copia originale del progetto, ma si desidera crearne uno da un file ispac o dal catalogo di SSISDB.  
  
### <a name="to-import-a-project"></a>Per importare un progetto  
  
1.  In [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]scegliere **Nuovo** > **progetto** dal menu **File** .  
  
2.  Nell'area **Modelli installati** della finestra **Nuovo progetto** espandere **Business Intelligence**, quindi scegliere **Integration Services**.  
  
3.  Selezionare **Importazione guidata progetto di Integration Services** dall'elenco dei tipi di progetto.  
  
4.  Digitare un nome per il nuovo progetto da creare nella casella di testo **Nome** .  
  
5.  Digitare il percorso del progetto nella casella di testo **Percorso** oppure fare clic su **Sfoglia** per selezionarne uno.  
  
6.  Digitare un nome per la soluzione nella casella di testo **Nome soluzione** .  
  
7.  Fare clic su **OK** per avviare la finestra di dialogo **Importazione guidata progetto di Integration Services** .  
  
8.  Fare clic su **Avanti** per passare alla pagina **Seleziona origine** .  
  
9. Se si importa da un file **ispac** , digitare il percorso comprendente il nome file nella casella di testo **Percorso** . Fare clic su **Sfoglia** per passare alla cartella in cui si desidera archiviare la soluzione e digitare il nome file nella casella di testo **Nome file** e fare clic su **Apri**.  
  
     Se si importa da un **Catalogo di Integration Services**, digitare il nome dell'istanza di database nella casella di testo **Nome server** oppure fare clic su **Sfoglia** e selezionare l'istanza di database che contiene il catalogo.  
  
     Fare clic su **Sfoglia** accanto alla casella di testo **Percorso** , espandere cartella nel catalogo, selezionare il progetto che si desidera importare e fare clic su **OK**.  
  
     Fare clic su **Avanti** per passare alla pagina **Verifica** .  
  
10. Rivedere le informazioni e fare clic su **Importa** per creare un progetto basato sul progetto esistente selezionato.  
  
11. Facoltativo: fare clic su **Salva report** per salvare i risultati in un file  
  
12. Fare clic su **Chiudi** per chiudere la finestra di dialogo **Importazione guidata progetto di Integration Services** .  
  
  
