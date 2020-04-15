---
title: Richiesta di informazioni di connessione all'utente Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282084"
---
# <a name="prompting-the-user-for-connection-information"></a>Chiedere all'utente informazioni di connessione
Se l'applicazione utilizza **SQLConnect** e deve richiedere all'utente le informazioni di connessione, ad esempio un nome utente e una password, deve farlo da solo. Mentre questo consente all'applicazione di controllare il suo "aspetto", potrebbe forzare l'applicazione a contenere codice specifico del driver. Ciò si verifica quando l'applicazione deve richiedere all'utente le informazioni di connessione specifiche del driver. Ciò presenta una situazione impossibile per le applicazioni generiche, che sono progettate per funzionare con tutti i driver, inclusi i driver che non esistono quando l'applicazione viene scritta.  
  
 **SQLDriverConnect** può richiedere all'utente le informazioni di connessione. Ad esempio, il programma personalizzato menzionato in precedenza potrebbe passare la stringa di connessione seguente a **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 Il driver potrebbe quindi visualizzare una finestra di dialogo che richiede ID utente e password, simile alla figura seguente.  
  
 ![Finestra di dialogo in cui vengono richiesti gli ID utente e le password](../../../odbc/reference/develop-app/media/pr18.gif "PR18 (informazioni in stato di")  
  
 Che il driver può richiedere informazioni di connessione è particolarmente utile per le applicazioni generiche e verticali. Queste applicazioni non devono contenere informazioni specifiche del driver e la richiesta del driver per le informazioni necessarie mantiene tali informazioni all'esterno dell'applicazione. Ciò è dimostrato dai due esempi precedenti. Quando l'applicazione ha passato solo il nome dell'origine dati al driver, l'applicazione non contiene informazioni specifiche del driver e pertanto non è stata legata a un driver specifico. Quando l'applicazione ha passato una stringa di connessione completa al driver, è stata legata al driver in grado di interpretare tale stringa.  
  
 Un'applicazione generica potrebbe fare un ulteriore passo avanti e non specificare nemmeno un'origine dati. Quando **SQLDriverConnect** riceve una stringa di connessione vuota, Gestione Driver visualizza la seguente finestra di dialogo.  
  
 ![Finestra di dialogo Seleziona origine dati](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Dopo che l'utente seleziona un'origine dati, Gestione Driver costruisce una stringa di connessione specificando tale origine dati e lo passa al driver. Il driver può quindi richiedere all'utente tutte le informazioni aggiuntive necessarie.  
  
 Le condizioni in cui il driver richiede all'utente sono controllate dal *DriverCompletion* flag; sono disponibili opzioni per richiedere sempre, richiedere se necessario o non richiedere mai. Per una descrizione completa di questo flag, vedere la descrizione della funzione [SQLDriverConnect.For](../../../odbc/reference/syntax/sqldriverconnect-function.md) a complete description of this flag, see the SQLDriverConnect function description.
