---
title: Connessione di attività e contenitori tramite un vincolo di precedenza predefinito | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b41330bcb2fe007b1f666382719f98d39ec67438
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921365"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>Connessione di attività e contenitori tramite un vincolo di precedenza predefinito
  Un vincolo di precedenza connette due eseguibili, che possono essere costituiti da qualsiasi attività oppure da un contenitore Ciclo For, Ciclo Foreach o Sequenza. Questa procedura descrive l'impostazione del comportamento predefinito dei vincoli di precedenza e la connessione di eseguibili tramite i vincoli di precedenza predefiniti.  
  
## <a name="creating-default-precedence-constraints"></a>Creazione dei vincoli di precedenza predefiniti  
 Al primo utilizzo di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] il valore predefinito di un vincolo di precedenza è `Success`. Eseguire la procedura seguente per configurare Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per l'utilizzo di un valore predefinito diverso per i vincoli di precedenza.  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>Per impostare il valore predefinito per i vincoli di precedenza  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Scegliere **Opzioni** dal menu **Strumenti**.  
  
3.  Nella finestra di dialogo **Opzioni** espandere **Finestre di progettazione Business Intelligence** e quindi espandere **Finestre di progettazione Integration Services**.  
  
4.  Fare clic su **Connessione automatica flusso di controllo** e selezionare **Per impostazione predefinita connetti la nuova forma alla forma selezionata**.  
  
5.  Nell'elenco a discesa selezionare **Usa vincolo Esito negativo per la nuova forma** oppure **Usa vincolo Completamento per la nuova forma**.  
  
6.  Fare clic su **OK**.  
  
#### <a name="to-create-a-default-precedence-constraint"></a>Per creare un vincolo di precedenza predefinito  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic sull'attività o sul contenitore e trascinarne il connettore fino all'eseguibile a cui si desidera applicare il vincolo di precedenza.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Vincoli di precedenza](control-flow/precedence-constraints.md)   
 [Impostare il valore di un vincolo di precedenza tramite il menu di scelta rapida](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Impostare le proprietà di un vincolo di precedenza](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Uso di un'espressione in un vincolo di precedenza](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
