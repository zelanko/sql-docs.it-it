---
title: Messaggi di errore (Driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31f894e58da93fe6091dba306f8b765d14bac2cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286401"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Messaggi di errore (driver ODBC Visual FoxPro)
Quando si verifica un errore, il driver Visual FoxPro restituisce le seguenti informazioni:  
  
-   Il numero di errore nativo e il testo del messaggio di errore  
  
-   SQLSTATE (un codice di errore ODBC) e testo del messaggio di errore  
  
 È possibile accedere a queste informazioni sull'errore chiamando [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errori nativi  
 Per gli errori che si verificano nell'origine dati, il driver Visual FoxPro restituisce il numero di errore nativo e il testo del messaggio di errore. Per un elenco dei numeri di errore nativi, vedere Messaggi di errore nativi del [driver ODBC di Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)  
 Per gli errori rilevati e restituiti dal driver Visual FoxPro, il driver esegue il mapping del numero di errore nativo restituito all'istruzione SQLSTATE appropriata. Se un numero di errore nativo non dispone di un codice di errore ODBC a cui eseguire il mapping, il driver Visual FoxPro restituisce SQLSTATE S1000 (errore generale).  
  
 Per un elenco dei valori SQLSTATE generati dal driver ODBC di Visual FoxPro per gli errori Visual FoxPro corrispondenti, vedere Codici di [errore ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintassi  
 I messaggi di errore hanno il seguente formato:  
  
 **[** *fornitore* **][** *ODBC_component* **]** *error_message*  
  
 I prefissi tra parentesi quadre ([ ]) identificano l'origine dell'errore come definito nella tabella seguente.  
  
|Origine dati|Prefisso|Valore|  
|-----------------|------------|-----------|  
|Gestione driver|[fornitore]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Gestione driver ODBC]<br />N/D|  
|Driver di Visual FoxPro|fornitore]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Driver ODBC Visual FoxPro]<br />N/D|  
  
 Ad esempio, se il driver ODBC di Visual FoxPro non riesce a trovare il file employee.dbf, potrebbe restituire il seguente messaggio di errore:  
  
 "[*Microsoft*][*ODBC Visual FoxPro Driver*]File 'employee.dbf' non esiste"
