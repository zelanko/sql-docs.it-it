---
title: Configurare un output degli errori in un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6f5db0ec29fb6900dbe74ea021f31d0afc5551d7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434888"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>Configurazione di un output degli errori in un componente del flusso di dati
  Molti componenti del flusso di dati supportano l'output degli errori. A seconda del componente, in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] sono disponibili strumenti diversi per la configurazione di un output degli errori. Oltre a configurare un output degli errori, è possibile configurare le relative colonne, tra cui le colonne **ErrorCode** e **ErrorColumn** aggiunte dal componente.  
  
## <a name="configuring-an-error-output"></a>Configurazione di un output degli errori  
 Per configurare un output degli errori sono disponibili due opzioni:  
  
-   Usare la finestra di dialogo **Configura output errori** . Questa finestra di dialogo consente di configurare un output degli errori in qualsiasi componente del flusso di dati che supporti l'output degli errori.  
  
-   Utilizzare la finestra di dialogo dell'editor per il componente. Alcuni componenti consentono di configurare gli output degli errori direttamente dalla finestra di dialogo dell'editor. Non è tuttavia possibile configurare output degli errori dalla finestra di dialogo dell'editor per l'origine ADO NET, la trasformazione Importa colonna, la trasformazione Comando OLE DB o la destinazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Nelle procedure seguenti viene descritto come utilizzare queste finestre di dialogo per configurare gli output degli errori.  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>Per configurare un output degli errori tramite la finestra di dialogo Configura output errori  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di dati** .  
  
4.  Trascinare l'output degli errori, rappresentato da una freccia rossa, dal componente corrispondente all'origine degli errori a un altro componente del flusso di dati.  
  
5.  Nella finestra di dialogo **Configura output errori** selezionare un'azione nelle colonne **Errore** e **Troncamento** per ogni colonna dell'input del componente.  
  
6.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>Per aggiungere un output degli errori tramite la finestra di dialogo dell'editor per il componente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di dati** .  
  
4.  Fare doppio clic sui componenti del flusso di dati in cui si desidera configurare un output degli errori e, a seconda del componente, eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Configura output errori**.  
  
    -   Fare clic su **Output degli errori**.  
  
5.  Impostare l'opzione **Errore** per ogni colonna.  
  
6.  Impostare l'opzione **Troncamento** per ogni colonna.  
  
7.  Fare clic su **OK**.  
  
8.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
## <a name="configuring-error-output-columns"></a>Configurazione delle colonne dell'output degli errori  
 Per configurare le colonne dell'output degli errori, è necessario usare la scheda **Proprietà input e output** della finestra di dialogo **Editor avanzato** .  
  
#### <a name="to-configure-error-output-columns"></a>Per configurare le colonne dell'output degli errori  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di dati** .  
  
4.  Fare clic con il pulsante destro del mouse sul componente di cui si desidera configurare le colonne dell'output degli errori, quindi scegliere **Visualizza editor avanzato**.  
  
5.  Fare clic sulla scheda **Proprietà input e output** , espandere ** \<component name> output errori** , quindi espandere **colonne di output**.  
  
6.  Fare clic su una colonna e aggiornarne le proprietà.  
  
    > [!NOTE]  
    >  L'elenco di colonne include le colonne dell'input del componente, le colonne **ErrorCode** e **ErrorColumn** aggiunte dall'output degli errori precedente e le colonne **ErrorCode** e **ErrorColumn** aggiunte dal componente corrente.  
  
7.  Fare clic su **OK**.  
  
8.  Per salvare il pacchetto aggiornato, dal menu **File** scegliere **Salva elementi selezionati**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli errori nei dati](data-flow/error-handling-in-data.md)  
  
  
