---
title: Appendice - 1 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 521c94fe15c8409377997edfc0b5821f92bed34d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759638"
---
# <a name="appendix---1-accesstosql"></a>Appendix - 1 (AccessToSQL)
Panoramica della Console SSMA opzioni riga di comando:  
  
|Sl. No.|Opzione|Obbligatorio?|Argomento parametro|Valori consentiti|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Yes|scriptfile|Nome file XML valido.<br /><br />File di definizione di Script della console.|  
|2|-v/variable|No|variablevaluefile|Nome file XML valido. Se vengono usate nel file di script, è necessario specificare questo file.|  
|3|-c/serverconnection|No|serverconnectionfile|Nome file XML valido. Questo file contiene informazioni di connessione server.|  
|4|-x/xmloutput|No|xmloutputfile|Questa opzione indica l'output di console in formato XML. Se questa opzione non è specificata, l'output predefinito è in formato testo.<br /><br />Se non viene specificato xmloutputfile, output XML viene indirizzato a STDOUT.<br /><br />Xmloutputfile è il nome del file in cui viene scritto l'output della console in formato XML.|  
|5|-l/log|No|logfile|Nome file valido.|  
|6|-e/projectenvironment|no|projectenvironmentfolder|Nome di cartella valido che contiene file dell'ambiente di progetto SSMA.|  
|7|-p/securepassword|No|-un/aggiungere {< server_id > [,... n] &#124; tutti i} - c&#124;serverconnection < server-connection-file > [-v&#124;variabile di < variabile-valore-file >] [-o/sovrascriverà]<br /><br />o Gestione configurazione<br /><br />-un/aggiungere {< server_id > [,... n] &#124; tutti i} -s&#124;script < file di script > [-v&#124;variabile di < variabile-valore-file >] [-o/sovrascriverà]<br /><br />-r/Rimuovi {< server_id > [,... n] &#124; tutti}<br /><br />-l/list<br /><br />/ esportazione di e-{< server-id > [,... n] &#124; tutti i} < crittografati-password - file ><br /><br />-i / Importa {< server-id > [,... n] &#124; tutti i} < crittografati-password-file >|Se specificato, questa opzione non deve essere eseguita con qualsiasi altra opzione.<br /><br />server-id: Un ID univoco fornito per un server {string}<br /><br />file di connessione server: file di definizione del server (serverconnectionfile o scriptfile).<br /><br />file di valore variabile: È un file di definizione di variabile e usato nel file di connessione server.<br /><br />encrypted-password-file: È un file server di password crittografato con una specificata dall'utente-passphrase.|  
|8|-?|No|Non applicabile|Non applicabile|  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della Console SSMA (accesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
