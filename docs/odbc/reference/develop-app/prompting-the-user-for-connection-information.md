---
title: Richiesta di informazioni di connessione all'utente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282084"
---
# <a name="prompting-the-user-for-connection-information"></a>Chiedere all'utente informazioni di connessione
Se l'applicazione usa **SQLConnect** ed è necessario richiedere all'utente le informazioni di connessione, ad esempio un nome utente e una password, questa operazione deve essere eseguita automaticamente. Sebbene ciò consenta all'applicazione di controllare il proprio aspetto, potrebbe forzare l'applicazione a contenere codice specifico del driver. Questo errore si verifica quando l'applicazione deve richiedere all'utente le informazioni di connessione specifiche del driver. Si tratta di una situazione impossibile per le applicazioni generiche, progettate per funzionare con tutti i driver, inclusi i driver che non esistono durante la scrittura dell'applicazione.  
  
 **SQLDriverConnect** può richiedere all'utente le informazioni di connessione. Ad esempio, il programma personalizzato indicato in precedenza potrebbe passare la stringa di connessione seguente a **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 Il driver potrebbe quindi visualizzare una finestra di dialogo in cui vengono richiesti gli ID utente e le password, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo in cui vengono richiesti gli ID utente e le password](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Che il driver possa richiedere informazioni di connessione è particolarmente utile per le applicazioni generiche e verticali. Queste applicazioni non devono contenere informazioni specifiche del driver e la richiesta del driver per le informazioni necessarie consente di mantenere le informazioni all'esterno dell'applicazione. Questa operazione viene illustrata nei due esempi precedenti. Quando l'applicazione ha passato solo il nome dell'origine dati al driver, l'applicazione non conteneva informazioni specifiche del driver e pertanto non era collegata a un driver specifico. Quando l'applicazione ha passato una stringa di connessione completa al driver, era collegata al driver che poteva interpretare tale stringa.  
  
 Un'applicazione generica può eseguire ulteriormente questo passaggio e non specificare neanche un'origine dati. Quando **SQLDriverConnect** riceve una stringa di connessione vuota, gestione driver Visualizza la finestra di dialogo seguente.  
  
 ![Finestra di dialogo Seleziona origine dati](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Dopo che l'utente ha selezionato un'origine dati, gestione driver crea una stringa di connessione che specifica l'origine dati e la passa al driver. Il driver può quindi richiedere all'utente informazioni aggiuntive necessarie.  
  
 Le condizioni in base alle quali il driver richiede che l'utente sia controllato dal flag *DriverCompletion* . sono disponibili opzioni per richiedere sempre, richiedere se necessario o mai chiedere conferma. Per una descrizione completa di questo flag, vedere la descrizione della funzione [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .
