---
title: "Attività 14: aggiunta dell'attività Esegui SQL al flusso di controllo per eseguire la stored procedure per MDS | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8c926f2ea3d9ef9973f75764e254c5e0884836e3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177291"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Attività 14: Aggiunta dell'Attività Esegui SQL al flusso di controllo per eseguire la stored procedure per MDS
  Dopo il caricamento dei dati nelle tabelle di staging MDS, eseguire una stored procedure associata alla tabella in questione per caricare i dati di staging nelle tabelle appropriate del database MDS. In questa stored procedure sono inclusi due parametri obbligatori che è necessario passare: LogFlag e VersionName. Il parametro LogFlag specifica se le transazioni vengono registrate durante il processo di gestione temporanea, mentre il parametro VersionName rappresenta la versione del modello. Per ulteriori informazioni, vedere l'argomento [stored procedure](https://msdn.microsoft.com/library/hh231028.aspx) di gestione temporanea.

 In questa attività viene aggiunta Attività Esegui SQL al flusso di controllo per richiamare la stored procedure in modo da caricare i dati di gestione temporanea nelle tabelle MDS appropriate.

1.  Passare ora alla scheda **flusso di controllo** .

2.  Trascinare l' **attività Esegui SQL** dalla **casella degli strumenti SSIS** alla scheda **flusso di controllo** .

3.  Fare clic con il pulsante destro del mouse su **attività Esegui SQL** nella scheda **flusso di controllo** e scegliere **Rinomina**. Digitare **trigger stored procedure per caricare i dati in MDS** e premere **invio**.

4.  Connettere **Ricevi, Pulisci, abbina e cura i dati fornitore** per **attivare la stored procedure per caricare i dati** usando il connettore verde.

     ![Connessione all'attività Esegui SQL](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "Connessione all'attività Esegui SQL")

5.  Usando la finestra **variabili** aggiungere due nuove variabili con le impostazioni seguenti. Se non viene visualizzata la finestra **variabili** , fare clic su **SSIS** sulla barra dei menu e fare clic su **variabili**.

    |Nome|Tipo di dati|valore|
    |----------|---------------|-----------|
    |LogFlag|Int32|1|
    |VersionName|string|VERSION_1|

     ![Finestra Variabili SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "Finestra Variabili SSIS")

6.  Fare doppio clic su **trigger stored procedure per caricare i dati in MDS**.

7.  Nella finestra di dialogo **Editor attività Esegui SQL** selezionare **(locale). MDS** (o **localhost). MDS**) per la **connessione**.

8.  Digitare **exec [STG]. [ udp_Supplier_Leaf]?,?,?** per l' **istruzione SQL**. Per verificare il nome, utilizzare SQL Server Management Studio.

     ![Finestra di dialogo Editor Esegui SQL - Impostazioni generali](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "Finestra di dialogo Editor Esegui SQL - Impostazioni generali")

9. Fare clic su **Mapping parametri** dal menu a sinistra.

10. Nella pagina **Mapping parametri** fare clic su **Aggiungi** per aggiungere un mapping. Ingrandire la finestra e ridimensionare le colonne in modo da visualizzare correttamente i valori negli elenchi a discesa.

11. Selezionare **User:: VersionName** dall'elenco a discesa per il nome della **variabile**.

12. Selezionare **nvarchar** per **tipo di dati**.

13. Digitare **0** (zero) per **nome parametro**.

14. Ripetere i quattro passaggi precedenti per aggiungere altre due variabili.

    |Nome variabile|Tipo di dati (importante)|Nome parametro|
    |-------------------|-----------------------------|--------------------|
    |User::LogFlag|LONG|1|
    |User::BatchTag|NVARCHAR|2|

     ![Editor attività Esegui SQL - Mapping parametri](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "Editor attività Esegui SQL - Mapping parametri")

15. Fare clic su **OK** per chiudere la finestra di dialogo **Editor SQL Esegui** .

## <a name="next-step"></a>passaggio successivo
 [Attività 15: Compilazione ed esecuzione del progetto SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)


