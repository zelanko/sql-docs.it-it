---
title: SQLDriverConnect (driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e270f8c9be42dc109adeaa49acb84f29f2b9511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307092"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Si connette a un'origine dati esistente, che può essere un [database](../../odbc/microsoft/visual-foxpro-terminology.md) o una directory di [tabelle libere.](../../odbc/microsoft/visual-foxpro-terminology.md) Le parole chiave dell'attributo ODBC UID e PWD vengono ignorate. Nella tabella seguente sono elencate le parole chiave di attributo supportate aggiuntive.  
  
|Parola chiave dell'attributo ODBC|Valore di attributo|  
|----------------------------|---------------------|  
|DSN||  
|UID|Ignorato dal driver ODBC di Visual FoxPro ma non genera un errore.|  
|PWD|Ignorato dal driver ODBC di Visual FoxPro ma non genera un errore.|  
|Driver|Il nome e il percorso del driver ODBC di Visual FoxPro; implementato da Gestione Driver.|  
  
|Parola chiave dell'attributo Driver ODBC di Visual FoxPro|Valore di attributo|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Sì" o "No"|  
|Fascicola|"Machine" o altra sequenza di confronto. Per un elenco delle sequenze di confronto supportate, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).|  
|Descrizione||  
|Esclusivo|"Sì" o "No"|  
|SourceDB|Percorso completo di una directory contenente zero o più [tabelle libere](../../odbc/microsoft/visual-foxpro-terminology.md)oppure il percorso assoluto e il nome file di un [database.](../../odbc/microsoft/visual-foxpro-terminology.md)|  
|SourceType|"DBC" o "DBF"|  
|Versione||  
  
 Se il nome dell'origine dati non è specificato, Gestione Driver richiede all'utente le informazioni (a seconda dell'impostazione del *fDriverCompletion* argomento) e quindi continua. Se sono necessarie ulteriori informazioni, il driver ODBC di Visual FoxPro visualizza la finestra di dialogo di richiesta.  
  
 Per ulteriori informazioni, vedere [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) in *ODBC Programmer's Reference*.
