---
description: Finestra di dialogo di configurazione ODBC Visual FoxPro
title: Finestra di dialogo di installazione di Visual FoxPro ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60d65d23a3a72f0194145c9a567f274e2e07ff74
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194326"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Finestra di dialogo di configurazione ODBC Visual FoxPro
La finestra di dialogo di **installazione di ODBC Visual FoxPro** consente di aggiungere o modificare un'origine dati Visual FoxPro.  
  
 Per scaricare il driver, vedere [il sito di download del driver ODBC Visual FoxPro](/previous-versions/visualstudio/foxpro/mt490121(v=msdn.10)).  
  
## <a name="dialog-box-options"></a>Opzioni della finestra di dialogo  
 **Nome origine dati**  
 Digitare il nome che si desidera utilizzare per l'origine dati.  
  
 **Descrizione**  
 Digitare una descrizione per l'origine dati.  
  
 **Tipo di database**  
 Consente di scegliere il tipo di database a cui si desidera connettere l'origine dati.  
  
 **Database Visual FoxPro (. DBC**  
 Specifica che l'origine dati si connette a un [database](../../odbc/microsoft/visual-foxpro-terminology.md) Visual FoxPro (file con estensione DBC) e a tutte le tabelle e le viste locali nel database.  
  
 **Directory della tabella gratuita**  
 Specifica che l'origine dati si connette a una directory di [tabelle gratuite](../../odbc/microsoft/visual-foxpro-terminology.md). Le tabelle di [database](../../odbc/microsoft/visual-foxpro-terminology.md) nella stessa directory vengono ignorate dalle funzioni del catalogo ODBC quali [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). È possibile accedere alle tabelle di database tramite istruzioni SQL SELECT inviate tramite [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Percorso**  
 Consente di visualizzare il percorso e il nome del database o la directory delle tabelle libere a cui si connette l'origine dati.  
  
 **Sfoglia**  
 Consente di eseguire ricerche nel sistema e nella rete per il database o la directory a cui si desidera connettere l'origine dati.  
  
 **Opzioni**  
 Espande la finestra di dialogo in modo che sia possibile impostare le opzioni del driver ODBC Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequenza di fascicolazione**  
 Sequenza in cui vengono ordinati i campi. Le sequenze predefinite riflettono le sequenze supportate dalla versione in lingua del sistema operativo. Per un elenco delle sequenze di confronto supportate, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Se questa casella di controllo è selezionata, il driver apre il database Visual FoxPro esclusivamente quando si accede ai dati tramite l'origine dati. Gli altri utenti non possono accedere al database o alle tabelle del database mentre il database viene aperto in modo esclusivo. Le tabelle all'interno del database aperto in modo esclusivo vengono aperte come condivise. Per aprire una tabella esclusivamente, utilizzare il comando [imposta esclusivo](../../odbc/microsoft/set-exclusive-command.md) . Questa casella di controllo è disabilitata quando il **tipo di database** è impostato su **libera directory della tabella**.  
  
 **Null**  
 Determina se le colonne create con ALTER TABLE e CREATE TABLE supportano valori null. Se si imposta null su, INSERT-SQL inserisce un valore null in qualsiasi colonna non inclusa in un'istruzione INSERT-SQL... Clausola VALUE. Se null è disattivato, viene inserito uno spazio vuoto. È anche possibile controllare questa opzione tramite una stringa di connessione passata come nel codice seguente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminata**  
 Determina se vengono restituite righe contrassegnate come eliminate. È anche possibile controllare questa opzione tramite una stringa di connessione passata come nel codice seguente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Recuperare i dati in background**  
 Determina se i record verranno recuperati in background (recupero progressivo) o se l'applicazione rimarrà in attesa finché non vengono recuperati tutti i record nel set di risultati.