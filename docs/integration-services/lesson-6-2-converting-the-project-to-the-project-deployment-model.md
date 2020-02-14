---
title: 'Passaggio 2: Convertire il progetto nel modello di distribuzione del progetto | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0563ceff3185f856692292884fe63e79c16e4216
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295877"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>Lezione 6-2: Convertire il progetto nel modello di distribuzione del progetto

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa attività viene usata la Conversione guidata progetto di Integration Services per convertire il progetto nel modello di distribuzione del progetto.  
  
1.  Selezionare **Converti nel modello di distribuzione del progetto** dal menu **Progetto**.  
  
2.  Nella **pagina introduttiva** della **Conversione guidata progetto di Integration Services** verificare i passaggi e quindi selezionare **Avanti**.  
  
3.  Nella pagina **Seleziona pacchetti** deselezionare nell'elenco **Pacchetti** tutte le caselle di controllo, ad eccezione di **Lesson 6.dtsx** e quindi selezionare **Avanti**.  
  
4.  Nella pagina **Specifica proprietà del progetto** selezionare **Avanti**.  
  
5.  Nella pagina **Aggiorna attività Esegui pacchetto** selezionare **Avanti**.  
  
6.  Nella pagina **Seleziona configurazioni** assicurarsi che sia selezionato il pacchetto **Lesson 6.dtsx** nell'elenco **Configurazioni**, quindi selezionare **Avanti**.  
  
7.  Nella pagina **Crea parametri** verificare che sia selezionato il pacchetto **Lesson 6.dtsx**.  Verificare che l'**ambito** sia **Pacchetto** nell'elenco delle **proprietà di configurazione** e quindi selezionare **Avanti**.  
  
8.  Nella pagina **Configura parametri** verificare che i valori per **Nome** e **Valore** corrispondano a quelli specificati nella lezione 5 per i valori relativi a variabile e configurazione, quindi selezionare **Avanti**.  
  
9. Nel riquadro **Riepilogo** della pagina **Verifica** si noti che la procedura guidata ha usato le informazioni disponibili nel file di configurazione per impostare le **proprietà** da convertire.  
  
10. Selezionare **Converti**.  
  
    Al termine della conversione viene visualizzato un messaggio di avviso per indicare che le modifiche non vengono salvate finché non si salva il progetto. Selezionare **OK** per chiudere la finestra dell'avviso.  
  
11. Nella **Conversione guidata progetto di Integration Services** selezionare **Chiudi**.  
  
12. In **SQL Server Data Tools** selezionare il menu **File** e quindi **Salva** per salvare il pacchetto convertito.  
  
13. Selezionare la scheda **Parametri** e verificare se il pacchetto ora contiene un parametro per **VarFolderName**. Il valore del parametro è lo stesso percorso specificato per la cartella **New Sample Data** nel file di configurazione della lezione 5.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 3: Testare il pacchetto della lezione 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
