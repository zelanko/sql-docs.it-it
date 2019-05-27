---
title: Importazione guidata progetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1399b14ec9345b9ca312db463ba5e508d9b9bbe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058052"
---
# <a name="import-project-wizard"></a>Importazione guidata progetto
  Utilizzare l'importazione guidata progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per creare un nuovo progetto di Integration Services basato su uno esistente. Importare i progetti che sono già stati distribuiti nel catalogo di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o importare i progetti da un file di distribuzione del progetto (con estensione ispac).  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>Per creare un progetto basato su un progetto nel file .ispac o nel catalogo  
  
1.  Fare clic su **Nuovo**dal menu **File**, quindi fare clic su Progetto.  
  
2.  Espandere **Business Intelligence**e fare clic su **Integration Services**.  
  
3.  Selezionare **Importazione guidata di Integration Services** nel riquadro centrale, digitare un **nome** per la soluzione, il progetto e specificare la **cartella** per il progetto, quindi scegliere **OK**.  
  
     Vedere l' **Importazione guidata progetto di Integration Services**. Questa procedura guidata crea un nuovo progetto di Integration Services basato su uno esistente  
  
4.  Fare clic su **Avanti** sulla pagina **Introduzione** per vedere la pagina **Seleziona origine** .  
  
5.  Specificare se si desidera importare il progetto da un file con estensione ispac o da un catalogo.  
  
    -   Se si seleziona l'opzione **File distribuzione progetto** , specificare il percorso del file con estensione ispac.  
  
    -   Se si seleziona l'opzione **Catalogo di Integration Services** , specificare il nome dell'istanza del server di database nel quale esiste il catalogo e il percorso al progetto nel catalogo.  
  
6.  Fare clic su **Avanti** sulla pagina **Seleziona origine** per vedere la pagina **Esame funzionalità** . Rivedere le informazioni visualizzate sulla pagina sull'operazione di importazione che la procedura guidata eseguirà.  
  
7.  Fare clic su **Importa** per creare un nuovo progetto di Integration Services basato su quello selezionato.  
  
8.  La pagina **Risultati** deve visualizzare i risultati dall'operazione di importazione che la procedura guidata ha eseguito. Fare clic su **Salva report** per salvare il report in un file XML.  
  
9. Per chiudere la procedura guidata, fare clic su **Chiudi** .  
  
  
