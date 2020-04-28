---
title: Impostazione dei valori dei parametri | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fd57f4308fb72aca2f829ccb9d7b884c12546
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299831"
---
# <a name="setting-parameter-values"></a>Configurazione dei valori dei parametri
Per impostare il valore di un parametro, l'applicazione imposta semplicemente il valore della variabile associata al parametro. Non è importante quando questo valore è impostato, purché sia impostato prima dell'esecuzione dell'istruzione. L'applicazione può impostare il valore prima o dopo l'associazione della variabile e può modificare il valore tutte le volte che desidera. Quando l'istruzione viene eseguita, il driver recupera semplicemente il valore corrente della variabile. Questa operazione è particolarmente utile quando un'istruzione preparata viene eseguita più di una volta; l'applicazione imposta nuovi valori per alcune o tutte le variabili ogni volta che viene eseguita l'istruzione. Per un esempio, vedere [esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md), più indietro in questa sezione.  
  
 Se un buffer di lunghezza/indicatore è stato associato nella chiamata a **SQLBindParameter**, deve essere impostato su uno dei valori seguenti prima dell'esecuzione dell'istruzione:  
  
-   Lunghezza in byte dei dati nella variabile associata. Il driver controlla questa lunghezza solo se la variabile è di tipo carattere o binario (*ValueType* è SQL_C_CHAR o SQL_C_BINARY).  
  
-   SQL_NTS. I dati sono una stringa con terminazione null.  
  
-   SQL_NULL_DATA. Il valore dei dati è NULL e il driver ignora il valore della variabile associata.  
  
-   SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC. Il valore del parametro deve essere inviato con **SQLPutData**. Per ulteriori informazioni, vedere [invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md), più avanti in questa sezione.  
  
 Nella tabella seguente vengono illustrati i valori della variabile associata e il buffer di lunghezza/indicatore impostato dall'applicazione per un'ampia gamma di valori di parametro.  
  
|Parametro<br /><br /> value|Parametro<br /><br /> SQL<br /><br /> Tipo di dati|Variabile (C)<br /><br /> Tipo di dati|Valore in <br /><br /> Associato<br /><br /> Variabile|Valore in <br /><br /> lunghezza/indicatore<br /><br /> buffer [d]|  
|-------------------------|-----------------------------------------|----------------------------------|-------------------------------------|----------------------------------------------------|  
|"ABC"|SQL_CHAR|SQL_C_CHAR|ABC\0 [a]|SQL_NTS o 3|  
|10|SQL_INTEGER|SQL_C_SLONG|10|--|  
|10|SQL_INTEGER|SQL_C_CHAR|10 \ 0 [a]|SQL_NTS o 2|  
|13.00|SQL_TYPE_TIME|SQL_C_TYPE_TIME|13, 0, 0 [b]|--|  
|13.00|SQL_TYPE_TIME|SQL_C_CHAR|{t'13:00:00'} \ 0 [a], [c]|SQL_NTS o 14|  
|NULL|SQL_SMALLINT|SQL_C_SSHORT|--|SQL_NULL_DATA|  
  
 [a] "\ 0" rappresenta un carattere di terminazione null. Il carattere di terminazione null è necessario solo se il valore nel buffer di lunghezza/indicatore è SQL_NTS.  
  
 [b] i numeri in questo elenco sono i numeri archiviati nei campi della struttura TIME_STRUCT.  
  
 [c] la stringa utilizza la clausola di escape della data ODBC. Per altre informazioni, vedere [valori letterali data, ora e timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 [d] i driver devono sempre controllare questo valore per verificare se si tratta di un valore speciale, ad esempio SQL_NULL_DATA.  
  
 Il funzionamento di un driver con un valore del parametro in fase di esecuzione dipende dal driver. Se necessario, il driver converte il valore dal tipo di dati C e la lunghezza in byte della variabile associata al tipo di dati SQL, alla precisione e alla scala del parametro. Nella maggior parte dei casi, il driver invia il valore all'origine dati. In alcuni casi, il valore viene formattato come testo e inserito nell'istruzione SQL prima di inviare l'istruzione all'origine dati.
