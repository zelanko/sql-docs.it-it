---
title: Copia colonna - trasformazione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6023db6e91b7d689afe621b23b6b0654ff70d985
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290427"
---
# <a name="copy-column-transformation"></a>Copia colonna - trasformazione
  La trasformazione Copia colonna consente di creare nuove colonne copiando le colonne di input e aggiungendo le nuove colonne all'output della trasformazione. Successivamente nel flusso di dati alle copie delle colonne sarà possibile applicare altre trasformazioni. È ad esempio possibile utilizzare la trasformazione Copia colonna per creare una copia di una colonna e quindi utilizzare la trasformazione Mappa caratteri per convertire in caratteri maiuscoli i dati copiati oppure utilizzare la trasformazione Aggregazione per applicare aggregazioni alla nuova colonna.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configurazione della trasformazione Copia colonna  
 Per configurare la trasformazione Copia colonna, è necessario specificare le colonne di input da copiare. È possibile creare più copie di una stessa colonna oppure creare copie di più colonne in una singola operazione.  
  
 Questa trasformazione include un input e un output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="copy-column-transformation-editor"></a>Editor trasformazione Copia colonna
  La finestra di dialogo **Editor trasformazione Copia colonna** consente di selezionare le colonne da copiare e di assegnare nomi alle nuove colonne di output.  
  
> [!NOTE]  
>  Quando si copiano tutti i dati di origine in una destinazione, potrebbe non essere necessario utilizzare la trasformazione Copia colonna. In alcuni casi è possibile connettere un'origine direttamente a una destinazione qualora non sia necessaria alcuna trasformazione dei dati. In simili circostanze è spesso preferibile utilizzare l'Importazione/Esportazione guidata SQL Server per creare automaticamente il pacchetto. Successivamente è possibile perfezionare e riconfigurare il pacchetto in base alle necessità. Per altre informazioni, vedere [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne da copiare mediante le caselle di controllo. Le selezioni effettuate determinano l'aggiunta delle colonne di input nella tabella sottostante.  
  
 **Colonna di input**  
 Consente di selezionare le colonne da copiare nell'elenco delle colonne di input disponibili. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo nella tabella **Colonne di input disponibili** .  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito **Copia di**seguito dal nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
