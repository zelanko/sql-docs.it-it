---
title: Impostazione dei valori di parametro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter values [ODBC]
ms.assetid: 13e5da79-b60c-48d0-b467-773f481ef2a4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66811d2364db546c3bddd787c1e0794f936f97c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445953"
---
# <a name="setting-parameter-values"></a>Configurazione dei valori dei parametri
Per impostare il valore di un parametro, l'applicazione imposta semplicemente il valore della variabile associata al parametro. Non è importante quando questo valore è impostato, fino a quando è impostato prima che venga eseguita l'istruzione. L'applicazione può impostare il valore prima o dopo l'associazione della variabile e può cambiare il valore come tutte le volte che desidera. Quando viene eseguita l'istruzione, il driver recupera semplicemente il valore corrente della variabile. Ciò è particolarmente utile quando viene eseguita un'istruzione preparata più volte. l'applicazione imposta nuovi valori per alcune o tutte le variabili ogni volta che viene eseguita l'istruzione. Per un esempio di questo oggetto, vedere [esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md), più indietro in questa sezione.  
  
 Se è stato associato un buffer di lunghezza/indicatore nella chiamata a **SQLBindParameter**, deve essere impostata su uno dei seguenti valori prima dell'esecuzione dell'istruzione:  
  
-   La lunghezza in byte dei dati nella variabile associata. Il driver controlla questa lunghezza solo se la variabile è character o binary (*ValueType* è SQL_C_CHAR o SQL_C_BINARY).  
  
-   SQL_NTS. I dati sono una stringa con terminazione null.  
  
-   SQL_NULL_DATA. Il valore dei dati è NULL e il driver ignora il valore della variabile associata.  
  
-   SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC. Il valore del parametro è venga inviato con **SQLPutData**. Per altre informazioni, vedere [l'invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md), più avanti in questa sezione.  
  
 Nella tabella seguente mostra i valori di variabile associata e il buffer di lunghezza/indicatore che consente di impostare l'applicazione per un'ampia gamma di valori di parametro.  
  
|Parametro<br /><br /> Valore|Parametro<br /><br /> (SQL)<br /><br /> Tipo di dati|Variable (C)<br /><br /> Tipo di dati|Valore in<br /><br /> Associato<br /><br /> variabile|Valore in<br /><br /> lunghezza/indicatore<br /><br /> buffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0[a]|SQL_NTS o 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10\0[a]|SQL_NTS o 2|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13,0,0[b]|--|  
|1 P.M.|SQL_TYPE_TIME|SQL_C_CHAR|{t ' 13: 00:00'} \0 [a], [c]|SQL_NTS oppure 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\0" rappresenta un carattere di terminazione null. Il carattere di terminazione null è necessario solo se il valore nel buffer di lunghezza/indicatore è SQL_NTS.  
  
 [b] i numeri in questo elenco sono i numeri memorizzati nei campi della struttura TIME_STRUCT.  
  
 [c] la stringa viene utilizzata la clausola di escape ODBC date. Per altre informazioni, vedere [Date, Time e Timestamp valori letterali](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] driver necessario controllare sempre questo valore per verificare se è un valore speciale, ad esempio SQL_NULL_DATA.  
  
 Funzionamento di un driver con un valore di parametro in fase di esecuzione dipende dal driver. Se necessario, il driver converte il valore dalla C byte e tipo lunghezza dei dati nella variabile associata per il tipo di dati SQL, precisione e scala del parametro. Nella maggior parte dei casi, il driver invia quindi il valore per l'origine dati. In alcuni casi, viene formattato il valore come testo e lo inserisce nell'istruzione SQL prima di inviare l'istruzione all'origine dati.
