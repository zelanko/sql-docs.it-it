---
title: Messaggi di errore (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286401"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>Messaggi di errore (driver ODBC Visual FoxPro)
Quando si verifica un errore, il driver Visual FoxPro restituisce le informazioni seguenti:  
  
-   Il numero di errore nativo e il testo del messaggio di errore  
  
-   Il valore SQLSTATE (codice di errore ODBC) e il testo del messaggio di errore  
  
 Per accedere a queste informazioni sull'errore, chiamare [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md).  
  
## <a name="native-errors"></a>Errori nativi  
 Per gli errori che si verificano nell'origine dati, il driver Visual FoxPro restituisce il numero di errore nativo e il testo del messaggio di errore. Per un elenco di numeri di errore nativi, vedere [messaggi di errore nativi del driver ODBC Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md).  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (codici di errore ODBC)  
 Per gli errori rilevati e restituiti dal driver Visual FoxPro, il driver esegue il mapping del numero di errore nativo restituito all'SQLSTATE appropriato. Se un numero di errore nativo non dispone di un codice di errore ODBC a cui eseguire il mapping, il driver Visual FoxPro restituisce SQLSTATE S1000 (errore generale).  
  
 Per un elenco di valori SQLSTATE generati dal driver ODBC Visual FoxPro per gli errori Visual FoxPro corrispondenti, vedere [codici di errore ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).  
  
## <a name="syntax"></a>Sintassi  
 Il formato dei messaggi di errore è il seguente:  
  
 **[** *Fornitore* **] [** *ODBC_component* **]** *ERROR_MESSAGE*  
  
 I prefissi tra parentesi quadre ([]) identificano l'origine dell'errore come definito nella tabella seguente.  
  
|Origine dati|Prefisso|valore|  
|-----------------|------------|-----------|  
|Gestione driver|fornitore<br />[ODBC_component]<br />[data_source]|Microsoft<br />[Gestione driver ODBC]<br />N/D|  
|Driver Visual FoxPro|fornitore<br />[ODBC_component]<br />[data_source]|Microsoft<br />[Driver ODBC Visual FoxPro]<br />N/D|  
  
 Se, ad esempio, il driver ODBC Visual FoxPro non è stato in grado di trovare il file Employee. dbf, potrebbe essere restituito il seguente messaggio di errore:  
  
 "[*Microsoft*] [*driver ODBC Visual FoxPro*] il file ' Employee. dbf ' non esiste"
