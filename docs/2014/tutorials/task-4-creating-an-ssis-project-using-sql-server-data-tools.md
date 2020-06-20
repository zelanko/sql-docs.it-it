---
title: 'Attività 4: creazione di un progetto SSIS con SQL Server Data Tools | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 935409eeb7724f4c9807aecc8ec69c4cba0735a1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006503"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>Attività 4: Creazione di un progetto SSIS tramite SQL Server Data Tools
  In questa attività viene creato un progetto SSIS utilizzando **SQL Server Data Tools** per automatizzare la pulizia e la corrispondenza dei dati fornitore.

1.  Avviare **SQL Server Data Tools**. Fare clic sul pulsante Start, scegliere **tutti i programmi**, espandere **Microsoft SQL Server 2012**e fare clic su **SQL Server Data Tools**.

2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.

3.  Espandere **Business Intelligence** nel riquadro **modelli installati** e selezionare **Integration Services**.

     ![Visual Studio - Finestra di dialogo Nuovo progetto](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - Finestra di dialogo Nuovo progetto")

4.  Selezionare **Integration Services progetto** nell' **elenco dei tipi di progetto**.

5.  Digitare **CleanseAndCurateSuppliers** per **nome** e fare clic su **OK**.

6.  Nella finestra **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Package. dtsx** e scegliere **Rinomina**. Se non viene visualizzata **Esplora soluzioni** finestra, fare clic su **Visualizza** nella barra dei menu e fare clic su **Esplora soluzioni**.

     ![Package.dtsx - Menu Rinomina](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx - Menu Rinomina")

7.  Digitare **CleanseAndCurate. dtsx** e premere **invio**. Verificare che l' **estensione** rimanga **. dtsx**.

## <a name="next-step"></a>passaggio successivo
 [Attività 5: Aggiunta dell'attività Flusso di dati](task-5-adding-data-flow-task.md)


