---
title: Chiedere conferma all'utente le informazioni di connessione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dfc63aaa6f162d382d6d8b3c627ff078c76825c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079062"
---
# <a name="prompting-the-user-for-connection-information"></a>Chiedere all'utente informazioni di connessione
Se l'applicazione usa **SQLConnect** e deve richiedere all'utente le informazioni di connessione, ad esempio un nome utente e password, è necessario farlo se stesso. Mentre in questo modo l'applicazione di controllare il relativo "aspetto", potrebbe forzare l'applicazione contenga codice specifico del driver. Ciò si verifica quando l'applicazione deve richiedere all'utente le informazioni di connessione specifici del driver. Questa operazione presenta una situazione di comunicazione Impossibile per applicazioni generiche, che sono progettati per funzionare con tutti i driver, inclusi i driver che non esistono quando l'applicazione è scritta.  
  
 **SQLDriverConnect** può chiedere all'utente le informazioni di connessione. Ad esempio, il programma personalizzato indicato in precedenza è stato possibile passare la stringa di connessione seguenti per **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 Il driver può quindi visualizzare una finestra di dialogo che richiede gli ID utente e password, simile alla figura seguente.  
  
 ![Finestra di dialogo che richiede gli ID utente e password](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Che il driver può richiedere le informazioni di connessione è particolarmente utile per le applicazioni verticali e non generici. Queste applicazioni non devono contenere informazioni specifiche del driver e avere il prompt dei comandi di driver per le informazioni che necessarie mantiene queste informazioni dall'applicazione. Come illustrato nei due esempi precedenti. Quando l'applicazione passati solo il nome dell'origine dati del driver, l'applicazione non contiene le informazioni specifiche del driver e non è stato pertanto associato a un driver specifico. Quando l'applicazione passata una stringa di connessione completa al driver, quest'ultima è stata associata al driver che è stato possibile interpretare tale stringa.  
  
 Un'applicazione generica potrebbe essere migliorano ulteriormente questo passaggio e non lo è nemmeno specificare un'origine dati. Quando **SQLDriverConnect** riceve una stringa di connessione vuota, il Driver Manager visualizza la finestra di dialogo seguente.  
  
 ![Finestra di dialogo Selezione origine dati](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Dopo che l'utente seleziona un'origine dati, gestione Driver costruisce una stringa di connessione che specifica tale origine dati e li passa al driver. Il driver può quindi richiedere all'utente le eventuali informazioni aggiuntive che necessarie.  
  
 Le condizioni in base alle quali il driver richiede all'utente vengono controllate per le *DriverCompletion* flag; sono disponibili le opzioni per Chiedi sempre conferma, chiederà di specificare se necessario, visualizzare mai la richiesta. Per una descrizione completa di questo flag, vedere la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.
