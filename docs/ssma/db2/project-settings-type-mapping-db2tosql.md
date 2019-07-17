---
title: Impostazioni progetto (Mapping di tipo) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7c0866a753bb61cb688ffe491e1de77431ddcb22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060165"
---
# <a name="project-settings-type-mapping-db2tosql"></a>Impostazioni progetto (Mapping di tipo) (DB2ToSQL)
La pagina del mapping dei tipi dei **impostazioni del progetto** finestra di dialogo contiene impostazioni che Personalizza modalità di conversione di tipi di dati DB2 in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i tipi di dati.  
  
La pagina del mapping dei tipi è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Per specificare le impostazioni per tutti i progetti SSMA futuri, nelle **Tools** menu fare clic su **impostazioni di progetto predefinite**, selezionare il tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati da **Versione di destinazione della migrazione** elenco a discesa e quindi fare clic su **Mapping dei tipi** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** menu fare clic su **le impostazioni del progetto**e quindi fare clic su **mapping tra i tipi** nella parte inferiore del riquadro di sinistra.  
  
Per specificare le impostazioni per l'oggetto corrente o la classe di oggetti, usare il **Mapping dei tipi** scheda nella finestra di SSMA primaria.  
  
## <a name="options"></a>Opzioni  
La tabella seguente illustra il **Mapping dei tipi** opzioni della scheda:  
  
**Tipo origine**  
Il tipo di dati DB2 mappato.  
  
**Tipo di destinazione**  
La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati per il tipo di dati DB2 specificato.  
  
Vedere le tabelle nella sezione successiva per il valore predefinito SSMA per i mapping dei tipi di DB2.  
  
**Aggiungi**  
Fare clic per aggiungere un tipo di dati all'elenco di mapping.  
  
**Modifica**  
Fare clic per modificare il tipo di dati selezionato nell'elenco di mapping.  
  
**Rimuovi**  
Fare clic per rimuovere il mapping dei tipi di dati selezionato dall'elenco di mapping.  
  
**Ripristina predefiniti**  
Fare clic per reimpostare l'elenco di mapping di tipo ai valori predefiniti di SSMA.  
  
## <a name="default-type-mappings"></a>Mapping dei tipi predefiniti  
In SSMA per DB2, è possibile impostare i mapping di tipi personalizzato per gli argomenti, colonne, variabili locali e valori restituiti. Il mapping predefinito per gli argomenti e tipi restituiti è quasi identico.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo di argomento predefinito e restituisce i Mapping dei tipi di valore  
Nella tabella seguente contiene il mapping dei tipi di dati predefinito per gli argomenti e valori restituiti.  
  
|DB2 Tipo di dati|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|BLOB|varbinary(max)|  
|boolean|bit|  
|char|ntext|  
|char varying|ntext|  
|character|ntext|  
|character varying|ntext|  
|Nell'oggetto CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|decimal|float [53]|  
|double precision|float [53]|  
|float|float [53]|  
|int|int|  
|integer|int|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [\*.. 8000]<sup>\*</sup>|varbinary[\*]|  
|long raw [8001 e..\*]<sup>\*</sup>|varbinary(max)|  
|National char|nvarchar(max)|  
|National char varying|nvarchar(max)|  
|caratteri nazionali|nvarchar(max)|  
|variabile di caratteri nazionali<sup>\*\*</sup>|nvarchar(max)|  
|variabile di caratteri nazionali<sup>\*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|ROWID|uniqueidentifier|  
|Signtype|smallint|  
|smallint|smallint|  
|string|ntext|  
|timestamp|datetime2|  
|timestamp con fuso orario locale|datetimeoffset|  
|timestamp con fuso orario|datetimeoffset|  
|UROWID|uniqueidentifier|  
|varchar|ntext|  
|Varchar2|ntext|  
|XmlType|xml|  
  
<sup>\*</sup> Si applica per restituire mapping solo di valori tipo.  
  
<sup>\*\*</sup> Si applica ai mapping solo di argomento tipo.  
  
### <a name="default-column-type-mapping"></a>Mapping dei tipi di colonna predefinito  
Nella tabella seguente contiene il mapping dei tipi predefiniti per le colonne.  
  
|DB2 Tipo di dati|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|BLOB|varbinary(max)|  
|char|char|  
|Char varying [\*.. \*]|varchar[\*]|  
|char[\*..\*]|char[\*]|  
|character|char|  
|variabili di carattere [\*.. \*]|varchar[\*]|  
|caratteri [\*.. \*]|char[\*]|  
|Nell'oggetto CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|dec[\*..\*]|dec[\*][0]|  
|dec[\*..\*][\*..\*]|dec[\*][\*]|  
|decimal|decimal[38][0]|  
|decimale [\*.. \*]|decimale [\*] [0]|  
|decimal[\*..\*][\*..\*]|decimal[\*][\*]|  
|double precision|float [53]|  
|float|float [53]|  
|float [\*.. 53]|float[\*]|  
|float[54..\*]|float [53]|  
|int|int|  
|integer|int|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [\*.. 8000]|varbinary[\*]|  
|long raw [8001 e..\*]|varbinary(max)|  
|long varchar|ntext|  
|tempo [\*.. 8000]|varchar[\*]|  
|long[8001..\*]|ntext|  
|National char|nchar|  
|National char varying [\*.. \*]|nvarchar[\*]|  
|National char [\*.. \*]|nchar[\*]|  
|caratteri nazionali|nchar|  
|variabile di caratteri nazionali [\*.. \*]|nvarchar[\*]|  
|caratteri nazionali [\*.. \*]|nchar[\*]|  
|nchar|nchar|  
|nchar[\*]|nchar[\*]|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|numero [\*.. \*]|numerico [\*]|  
|number[\*..\*][\*..\*]|numeric[\*][\*]|  
|numeric|numeric|  
|numeric[\*..\*]|numerico [\*]|  
|numeric[\*..\*][\*..\*]|numeric[\*][\*]|  
|nvarchar2[\*..\*]|nvarchar[\*]|  
|raw[\*..\*]|varbinary[\*]|  
|real|float [53]|  
|ROWID|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|timestamp con fuso orario locale|datetimeoffset|  
|timestamp con fuso orario locale [\*.. \*]|datetimeoffset[\*]|  
|timestamp con fuso orario|datetimeoffset|  
|timestamp con fusi orari [\*.. \*]|datetimeoffset[\*]|  
|timestamp [\*.. \*]|datetime2[\*]|  
|UROWID|uniqueidentifier|  
|urowid[\*..\*]|uniqueidentifier|  
|varchar[\*..\*]|varchar[\*]|  
|varchar2[\*..\*]|varchar[\*]|  
|XmlType|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Mapping dei tipi di variabile locale predefinito  
Nella tabella seguente contiene il mapping dei tipi predefiniti per le variabili locali.  
  
|DB2 Tipo di dati|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|Char varying [\*.. 8000]|varchar[\*]|  
|Char varying [8001 e..\*]|ntext|  
|Char [\*.. 8000]|char[\*]|  
|Char [8001 e..\*]|ntext|  
|Carattere|char|  
|variabili di carattere [\*.. 8000]|varchar[\*]|  
|variabili di carattere [8001 e..\*]|ntext|  
|caratteri [\*.. 8000]|char[\*]|  
|caratteri [8001 e..\*]|ntext|  
|Nell'oggetto CLOB|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|dec[\*..\*]|dec[\*][0]|  
|dec[\*..\*][\*..\*]|dec[\*][\*]|  
|decimal|decimal[38][0]|  
|decimale [\*.. \*]|decimale [\*] [0]|  
|decimal[\*..\*][\*..\*]|decimal[\*][\*]|  
|double precision|float [53]|  
|Float|float [53]|  
|float [\*.. 53]|float[\*]|  
|float[54..\*]|float [53]|  
|Int|int|  
|Integer|int|  
|numero intero [\*.. \*]|numerico [\*] [0]|  
|Long|ntext|  
|long raw|varbinary(max)|  
|long raw [\*.. 8000]|varbinary[\*]|  
|long raw [8001 e..\*]|varbinary(max)|  
|National char|nchar|  
|National char varying [\*.. 4000]|nvarchar[\*]|  
|National char varying [4001..\*]|nvarchar(max)|  
|National char [\*.. 4000]|nchar[\*]|  
|National char [4001..\*]|nvarchar(max)|  
|caratteri nazionali|nchar|  
|caratteri nazionali [\*.. 4000]|nvarchar[\*]|  
|caratteri nazionali [4001..\*]|nvarchar(max)|  
|variabile di caratteri nazionali [\*.. 4000]|nvarchar[\*]|  
|variabile di caratteri nazionali [4001..\*]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [\*.. 4000]|nchar[\*]|  
|nchar[4001..\*]|nvarchar(max)|  
|nchar varying [\*.. 4000]|nvarchar[\*]|  
|nchar varying [4001..\*]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Number|float [53]|  
|numero [\*.. \*]|numerico [\*]|  
|number[\*..\*][\*..\*]|numeric[\*][\*]|  
|Numeric|numerico [38] [0]|  
|numeric[\*..\*]|numerico [\*]|  
|numeric[\*..\*][\*..\*]|numeric[\*][\*]|  
|nvarchar2[\*..4000]|nvarchar[\*]|  
|nvarchar2[4001..\*]|nvarchar(max)|  
|pls_integer|int|  
|non elaborato [\*.. 8000]|varbinary[\*]|  
|raw[8001..\*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|stringa [\*.. 8000]|varchar[\*]|  
|stringa [8001 e..\*]|ntext|  
|timestamp|datetime2|  
|timestamp con fuso orario locale|datetimeoffset|  
|timestamp con fuso orario|datetimeoffset|  
|timestamp con fuso orario locale [\*.. \*]|datetimeoffset[\*]|  
|timestamp con fusi orari [\*.. \*]|datetimeoffset[\*]|  
|timestamp [\*.. \*]|datetime2[\*]|  
|UROWID|uniqueidentifier|  
|urowid[\*..\*]|uniqueidentifier|  
|varchar [\*.. 8000]|varchar[\*]|  
|varchar [8001 e..\*]|ntext|  
|varchar2[\*..8000]|varchar[\*]|  
|varchar2[8001..\*]|varcha(max)|  
|XmlType|xml|  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'interfaccia utente &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
