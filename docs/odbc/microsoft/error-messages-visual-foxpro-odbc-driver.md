---
title: I messaggi di errore (Driver ODBC Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6072a6e317ab87118376b08790fc0fb49c495e3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952512"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Messaggi di errore (driver ODBC Visual FoxPro)
Quando si verifica un errore, il driver di Visual FoxPro restituisce le informazioni seguenti:  
  
-   Il numero di errore nativo e il testo del messaggio di errore  
  
-   SQLSTATE (un codice di errore ODBC) e testo messaggio di errore  
  
 Accedere a queste informazioni di errore chiamando [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errori nativi  
 Per gli errori che si verificano nell'origine dati, il driver di Visual FoxPro restituisce il numero di errore nativo e il testo del messaggio di errore. Per un elenco di numeri di errori nativi, vedere [Visual FoxPro ODBC Driver Native i messaggi di errore](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)  
 Per gli errori che vengono rilevati e restituiti dal driver Visual FoxPro, il driver esegue il mapping il numero di errore nativo restituito al codice SQLSTATE appropriato. Se un numero di errori nativi non ha un codice di errore ODBC per eseguire il mapping, il driver di Visual FoxPro restituisce SQLSTATE S1000 (errore generale).  
  
 Per un elenco di valori SQLSTATE generati dal Driver ODBC Visual FoxPro per gli errori di Visual FoxPro corrispondenti, vedere [codici di errore ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintassi  
 I messaggi di errore hanno il formato seguente:  
  
 **[** *vendor* **][** *ODBC_component* **]** *error_message*  
  
 I prefissi tra parentesi quadre ([]) identificano l'origine dell'errore, come definito nella tabella seguente.  
  
|Origine dati|Prefisso|Value|  
|-----------------|------------|-----------|  
|Gestione driver|[produttore]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Gestione Driver ODBC]<br />N/D|  
|Driver Visual FoxPro|fornitore]<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[Driver ODBC Visual FoxPro]<br />N/D|  
  
 Ad esempio, se il Driver ODBC Visual FoxPro non è riuscito a trovare il file Employee. dbf, potrebbe restituire il messaggio di errore seguente:  
  
 "[*Microsoft*] [*Driver ODBC Visual FoxPro*] il File 'Employee. dbf' non esiste"
