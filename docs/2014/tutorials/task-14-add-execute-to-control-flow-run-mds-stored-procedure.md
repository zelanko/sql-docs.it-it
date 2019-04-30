---
title: 'Attività 14: Aggiunta di attività Esegui SQL al flusso di controllo per eseguire la Stored Procedure per MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf0a02e973d046f3dff2b2df95327cf38e88443c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222705"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Attività 14: Attività dell'attività Esegui SQL al flusso di controllo per eseguire la stored procedure per MDS
  Dopo il caricamento dei dati nelle tabelle di staging MDS, eseguire una stored procedure associata alla tabella in questione per caricare i dati di staging nelle tabelle appropriate del database MDS. Questa stored procedure ha due parametri obbligatori che è necessario passare: LogFlag e VersionName. Il parametro LogFlag specifica se le transazioni vengono registrate durante il processo di gestione temporanea, mentre il parametro VersionName rappresenta la versione del modello. Visualizzare [Stored Procedure di staging](https://msdn.microsoft.com/library/hh231028.aspx) per altre informazioni.  
  
 In questa attività viene aggiunta Attività Esegui SQL al flusso di controllo per richiamare la stored procedure in modo da caricare i dati di gestione temporanea nelle tabelle MDS appropriate.  
  
1.  Passare ora al **flusso di controllo** scheda.  
  
2.  Funzionalità di trascinamento **attività Esegui SQL** dal **casella degli strumenti SSIS** per il **flusso di controllo** scheda.  
  
3.  Fare doppio clic su **attività Esegui SQL** nel **flusso di controllo** scheda, quindi scegliere **rinominare**. Tipo di **avvia Stored Procedure per caricare i dati in MDS** , quindi premere **invio**.  
  
4.  Connettere **Ricevi, Pulisci, corrispondenza e dei dati fornitore abbina** al **avvia Stored Procedure per caricare i dati** usando il connettore verde.  
  
     ![Connettersi all'attività Esegui SQL](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "connettersi all'attività Esegui SQL")  
  
5.  Usando il **variabili** finestra, aggiungere due nuove variabili con le impostazioni seguenti. Se non viene visualizzato il **variabili** finestra, fare clic su **SSIS** nella barra dei menu e fare clic su **variabili**.  
  
    |Nome|Tipo di dati|Value|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![Finestra variabili SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "finestra variabili SSIS")  
  
6.  Fare doppio clic su **attivano Stored Procedure per caricare i dati in MDS**.  
  
7.  Nel **Editor attività Esegui SQL** finestra di dialogo **(locale). MDS** (o **localhost. MDS**) per **connessione**.  
  
8.  Tipo **EXEC [stg]. [ udp_Supplier_Leaf]?,?,?** per la **istruzione SQL**. Per verificare il nome, utilizzare SQL Server Management Studio.  
  
     ![Eseguire finestra di dialogo Editor SQL - impostazioni generali](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "eseguire finestra di dialogo Editor SQL - impostazioni generali")  
  
9. Fare clic su **Mapping parametri** nel menu a sinistra.  
  
10. Nel **Mapping dei parametri** pagina, fare clic su **Add** per aggiungere un mapping. Ingrandire la finestra e ridimensionare le colonne in modo da visualizzare correttamente i valori negli elenchi a discesa.  
  
11. Selezionare **User:: VersionName** nell'elenco a discesa per il **il nome di variabile**.  
  
12. Selezionare **NVARCHAR** per **tipo di dati**.  
  
13. Tipo di **0** (zero) per **nome del parametro**.  
  
14. Ripetere i quattro passaggi precedenti per aggiungere altre due variabili.  
  
    |Nome variabile|Tipo di dati (importante)|Nome parametro|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![Editor attività Esegui SQL - Mapping parametri](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "Editor attività Esegui SQL - Mapping parametri")  
  
15. Fare clic su **OK** per chiudere la **Editor Esegui SQL** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 15: Compilazione e l'esecuzione del progetto SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
