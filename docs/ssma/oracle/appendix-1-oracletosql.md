---
title: Appendice-1 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 85051c1138e2edd152ab5fce5b5a32f4ea6f297b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264528"
---
# <a name="appendix---1-oracletosql"></a>Appendice - 1 (OracleToSQL)
Visualizzazione rapida delle opzioni della riga di comando della console SSMA:  
  
|SL. No.|Opzione|Obbligatorio?|Argomento switch|Valori consentiti|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Sì|scriptfile|Nome file XML valido.<br /><br />File di definizione dello script della console.|  
|2|-v/variabile|No|variablevaluefile|Nome file XML valido.<br /><br />Se le variabili vengono usate nel file di script, è necessario specificare questo file.|  
|3|-c/ServerConnection|No|serverconnectionfile|Nome file XML valido.<br /><br />Questo file contiene le informazioni di connessione al server.|  
|4|-x/xmloutput|No|xmloutputfile|Questa opzione indica l'output della console in formato XML. Se questa opzione non è specificata, l'output predefinito è in formato testo.<br /><br />Se xmloutputfile non è specificato, l'output XML viene indirizzato a `STDOUT`.<br /><br />Xmloutputfile è il nome del file in cui viene scritto l'output della console in formato XML.|  
|5|-l/log|No|logfile|Nome file valido.|  
|6|-e/projectenvironment|No|projectenvironmentfolder|Nome di cartella valido contenente i file dell'ambiente del progetto SSMA.|  
|7|-p/SecurePassword|No|-a/Add {<server_id> [,... n] &#124; all}-c&#124;ServerConnection <Server-Connection-file> [-v&#124;variabile <variabile-valore-file>] [-o/Overwrite]<br /><br />o<br /><br />-a/Add {<server_id> [,... n] &#124; di tutti gli script&#124;}-s <script-file> [-v&#124;variabile <variabile-valore-file>] [-o/Sovrascrivi]<br /><br />-r/Remove {<server_id> [,... n] &#124; tutti}<br /><br />-l/elenco<br /><br />-e/Export {<Server-ID> [,... n] &#124; all} <encrypted-password-file><br /><br />-i/Import {<Server-ID> [,... n] &#124; all} <encrypted-password-file>|Se specificato, questa opzione non deve essere combinata con altre opzioni.<br /><br />Server-ID: un ID univoco fornito per un server {String}<br /><br />Server-Connection-File: file di definizione del server (serverconnectionfile o scriptfile).<br /><br />variable-value-file: si tratta di un file di definizione di variabile usato in Server-Connection-file.<br /><br />encrypted-password-file: si tratta di un file di password del server crittografato con una passphrase specificata dall'utente.|  
|8|-?|No|Non applicabile|Non applicabile|  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della console SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
